# @openbat/mcp

[Model Context Protocol](https://modelcontextprotocol.io) server for
OpenBat. Lets Claude Desktop, Cursor, or any MCP-aware client manage a
chatbot end-to-end — read conversations + analytics, manage settings +
webhooks + workflows + reports, and (with a PAT) create new chatbots
and run org-level operations.

The exposed tool surface **scales with credential strength** — start the
server with a read key and you get the read-only surface; start it with
an admin key and the per-chatbot write tools appear; start it with a PAT
and you also see chatbot-creation + org-level tools.

> **Companion docs**: [`@openbat/cli`](../cli/README.md) (same surface
> over CLI), [`lib/openbat-tools/`](../../lib/openbat-tools/README.md)
> (tool registry that powers both), and the
> [A-Z test guide](../../docs/agent-surface-testing.md).

## Install (zero-install — recommended)

You don't need to globally install anything. Configure your MCP client
to launch the server on demand via `npx`:

### Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json`
(macOS) or the equivalent on your platform:

```jsonc
{
  "mcpServers": {
    "openbat": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": {
        "OPENBAT_API_KEY": "ob_pat_..."
      }
    }
  }
}
```

Restart Claude Desktop. The OpenBat tools appear in the tool selector.

### Cursor

Cursor reads `.cursor/mcp.json` in your project, or `~/.cursor/mcp.json`
globally — same shape:

```jsonc
{
  "mcpServers": {
    "openbat": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": {
        "OPENBAT_API_KEY": "ob_pat_..."
      }
    }
  }
}
```

Reload Cursor.

### Other MCP clients

The server speaks stdio JSON-RPC. Any client that follows the
[MCP spec](https://spec.modelcontextprotocol.io) can launch it the same
way.

---

## Credential kind detection

The server inspects the prefix of `OPENBAT_API_KEY` at startup and:

1. **Refuses ingest keys** — `ob_live_*` is SDK-only; the server exits
   with `openbat-mcp: ob_live_* keys are SDK-only — use an ob_read_*,
   ob_admin_*, or ob_pat_* key instead.`
2. **Refuses malformed keys** — anything that doesn't match the four
   known prefixes is rejected before any tool is registered.
3. **Logs a startup banner** to stderr — `using <kind> key <prefix>…<hidden>, base <url>` — never the full plaintext.
4. **Filters the exposed tool list** by an "authority ranking" — see
   below.

### Authority ranking

`pat > admin > read`. A higher kind can call every tool a lower kind
can call. Each tool declares a `minKind`; the server's
`tools/list` response only includes tools whose `minKind` is ≤ the
resolved kind.

### Picking the right kind

| Goal | Key kind |
|---|---|
| Read-only dashboards / analytics for one chatbot | `ob_read_*` |
| Manage one chatbot's webhooks / workflows / reports / settings | `ob_admin_*` |
| Create new chatbots, mint admin keys, manage your orgs | `ob_pat_*` |

PATs also carry a per-row sub-scope (`read` or `admin`). A read-scope
PAT can run every read tool across every chatbot in your orgs but
cannot mutate anything — the server will surface the write tools but
the v1 routes will return 403.

---

## Pin to one chatbot (hard lock)

Set `OPENBAT_CHATBOT_ID` (or run `openbat use <id>` once — it writes
`~/.openbatrc`, which the server also reads) to lock the server to a single
chatbot. This is the safe default when a PAT can reach many. When pinned, the
server:

- **injects** the pinned `chatbotId` into every per-chatbot tool, and
  **rejects** a call that passes a different one;
- returns **only** the pinned chatbot from `openbat_list_chatbots`;
- **hides** cross-chatbot / org tools (`openbat_create_chatbot`,
  `openbat_list_orgs`, org members);
- verifies the pin against the key's reachable set at startup (exits if it
  isn't reachable) and logs `pinned to "<name>" (<id>)`.

```jsonc
{
  "mcpServers": {
    "openbat": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": { "OPENBAT_API_KEY": "ob_pat_...", "OPENBAT_CHATBOT_ID": "<uuid>" }
    }
  }
}
```

To switch: change `OPENBAT_CHATBOT_ID` (or `openbat use <other>`) and restart.
A chatbot-scoped `ob_read_*` / `ob_admin_*` key is single-chatbot by
construction, so the pin is automatic — nothing to set.

---

## What tools are exposed

All inputs are Zod-validated with `.strict()`, bounded ranges, and
explicit enums. Response size is capped at ~1MB.

### `read` minKind (visible to read / admin / pat)

| Tool | Description |
|---|---|
| `openbat_list_chatbots` | List every chatbot the key authorises (returns only the pinned one when pinned). Call this FIRST. |
| `openbat_get_chatbot` | DEPRECATED — use `openbat_list_chatbots`. Returns the full chatbot list. |
| `openbat_list_conversations` | Paginate recent conversations (page, limit ≤ 100, `from`/`to`, `kind`: organic-default / probe / all) |
| `openbat_get_conversation` | Fetch one conversation by UUID — messages + ALL analyses (issues/outcomes/flags/intents + reasoning + verification fields) |
| `openbat_await_analysis` | Poll a conversation's analysis progress; `allComplete`/`anyFailed` + per-message statuses. Accepts an internal UUID OR a probe's `obprobe_` id (resolves external→internal; `found:false` while capture is in flight). |
| `openbat_probe` | Start a synthetic eval turn — returns a reserved `obprobe_` conversationId + next steps. YOU send `message` to your chatbot with that id; then `openbat_await_analysis`; then `openbat_get_conversation` for the verdict. (OpenBat never calls your chatbot.) |
| `openbat_optimize_context` | One call: organic `review` (probe-excluded) + active prompt + analysis definitions together — bootstrap the eval loop without 3+ round trips. |
| `openbat_review` | Daily eval digest: outcome/sentiment deltas + top issues/flags/intents with representative pointers (`windowMinutes`, default 1440) |
| `openbat_analytics_overview` | Totals + sentiment distribution |
| `openbat_analytics_sentiment` | Sentiment over time (`days` 1–90) |
| `openbat_export_data` | Bulk export (`json` or `csv`) — capped at ~1MB |
| `openbat_list_webhooks` | List webhooks for a chatbot |
| `openbat_list_workflows` | List workflows for a chatbot |
| `openbat_list_reports` | List AI reports for a chatbot |
| `openbat_list_prompt_versions` | System-prompt versions + live controls (active version, kill switch) |
| `openbat_get_prompt_version` | Fetch one version's full template text by id |
| `openbat_get_active_prompt` | What the server resolves to right now (active version id, kill switch) |
| `openbat_get_backtest_status` | Poll a backtest's progress + verdict tally (keyed by backtestId) |
| `openbat_list_external_users` | External users + health metrics (defaults to last 7d) |

### `admin` minKind (visible to admin / pat)

| Tool | Description |
|---|---|
| `openbat_create_webhook` | Create a webhook (SSRF-validated; signing secret in response) |
| `openbat_delete_webhook` | Delete a webhook |
| `openbat_create_workflow_from_template` | Compile DSL template → workflow |
| `openbat_create_ai_report` | New AI report + org-private dashboard URL |
| `openbat_update_chatbot_settings` | Patch settings (allowlisted keys) |
| `openbat_publish_prompt` | Publish `templateText` as the LIVE system prompt (live in ~60s for fetch-endpoint chatbots) |
| `openbat_create_draft_prompt` | Create a prompt version WITHOUT activating it (a draft) — probe/eval it against a candidate, then activate. Returns the versionId. |
| `openbat_activate_prompt_version` | Point the live prompt at an existing version id (roll back/forward) |
| `openbat_set_prompt_kill_switch` | Toggle the remote prompt kill switch (fallback to hardcoded prompt) |

### `pat` minKind (visible to pat only)

| Tool | Description |
|---|---|
| `openbat_create_chatbot` | Mint a new chatbot in your primary org |
| `openbat_create_backtest` | Replay flagged conversations against a candidate prompt (attributed to the PAT's user) |
| `openbat_generate_admin_key` | Mint a fresh admin key for a chatbot |
| `openbat_list_orgs` | Orgs the PAT's user belongs to |
| `openbat_rename_org` | Rename an org (owner only) |
| `openbat_list_org_members` | Members of an org |
| `openbat_invite_org_member` | Invite a new member (note: email send is a follow-up) |

There are deliberately **no mutation tools for ingest keys** — those
remain SDK-only via `OpenBat.recordMessages`.

---

## Multi-kind config examples

### Read-only dashboard agent (CI)

```jsonc
{
  "mcpServers": {
    "openbat-readonly": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": { "OPENBAT_API_KEY": "ob_read_..." }
    }
  }
}
```

Tool selector shows the read-only tools (conversations, `review`, analytics, prompt-version listing, …).

### Admin agent for one chatbot

```jsonc
{
  "mcpServers": {
    "openbat-acme": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": { "OPENBAT_API_KEY": "ob_admin_..." }
    }
  }
}
```

Tool selector adds the per-chatbot write tools (webhooks, workflows,
reports, settings).

### Full-control agent (org admin + chatbot creator)

```jsonc
{
  "mcpServers": {
    "openbat-control": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": { "OPENBAT_API_KEY": "ob_pat_..." }
    }
  }
}
```

Tool selector also lights up `openbat_create_chatbot`,
`openbat_generate_admin_key`, and the org-level tools.

---

## Getting an API key

Generate the appropriate key in the OpenBat dashboard:
- `ob_read_*` → `Settings → API Keys → Generate Read key`
- `ob_admin_*` → `Settings → API Keys → Generate Admin key`
- `ob_pat_*` → `Settings → Personal Access Tokens`

The plaintext is shown exactly once.

The dashboard also has a **"Copy MCP config (with key)"** button on
each page — it pre-fills the JSON above so you can paste it straight
into Claude / Cursor.

---

## Security properties

- The API key is read from `OPENBAT_API_KEY` only — never from
  arguments or stdin, so it can't leak via shell history or process
  listings.
- Startup logs print the **resolved kind + 16-char prefix only** —
  plaintext never lands in any log.
- Every tool input is Zod-validated with strict shapes (`.strict()`),
  bounded numeric ranges, and explicit enums — an LLM that
  hallucinates extra args gets a clean validation error.
- The HTTP client refuses non-HTTPS base URLs except `localhost` /
  `127.0.0.1`.
- Response size cap (~1MB) on every tool — protects the LLM context
  window and limits damage if a prompt steers the LLM toward bulk
  exfil.
- Tool error messages are key-redacted (`ob_<kind>_…<hidden>`) before
  they reach the client.
- **Mint tools (admin keys, etc.) return plaintext exactly once** in
  the tool response. The LLM gets to see it. Skill prompts should
  instruct the assistant to surface it to the user immediately
  (see `using-openbat` skill).
- **Per-tool rate-limit buckets** server-side. 429 responses include
  `Retry-After`; the MCP tool error surfaces it. Stricter buckets:
  `create_chatbot` 5/hr per PAT, mint operations 10/hr per credential,
  `chat_ai_report` 30/min per credential.
- **Audit log** — every authenticated call (success and failure both)
  lands in `api_audit_log` (Supabase, migration 036). Operators can
  reconstruct exactly what an MCP-driven LLM did.
- **HTTP 401 vs 403** is meaningful: 401 → bad/expired/wrong-kind key
  (rotate via the dashboard); 403 → key valid but lacks permission
  (read-scope PAT trying to mutate, or non-owner trying an
  owner-only op).

---

## Override the base URL

For dogfooding against a local dev server:

```jsonc
{
  "mcpServers": {
    "openbat": {
      "command": "npx",
      "args": ["-y", "@openbat/mcp"],
      "env": {
        "OPENBAT_API_KEY": "ob_pat_...",
        "OPENBAT_BASE_URL": "http://localhost:3000"
      }
    }
  }
}
```

The server refuses non-HTTPS URLs unless they point at localhost.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `openbat-mcp: ob_live_* keys are SDK-only` | Pasted an ingest key | Generate a read/admin/PAT key instead |
| Tool not in `tools/list` | Your key kind is below the tool's `minKind` | Use a higher-kind key |
| `Tool X requires a Y key or higher` on call | Same as above, but client cached the list | Restart the client |
| 401 from a tool | Key invalid / expired / revoked | Rotate via the dashboard |
| 403 from a write tool | Read-scope PAT, or non-owner trying an owner action | Use admin-scope key or an owner credential |
| 404 on a chatbot id | Cross-org / not in scope (404 by design, no enumeration) | Pass the right id |
| 429 with `Retry-After` | Per-tool rate-limit hit | Wait the indicated seconds and retry |

---

## Pre-loaded context for AI assistants

If you're driving an AI agent through this MCP server, install the
OpenBat agent skill bundle so the agent loads the right procedural
knowledge (auth ladder, safe-mutation patterns, plaintext-only-once
conventions) into its context:

```bash
npx skills add openbat-dev/agent-skills
```

Drops the `SKILL.md` bundle into the target project. The
`using-openbat` skill is the comprehensive reference; the rest cover
per-flow specifics (onboarding, settings, conversations, workflows,
SDK install, the daily eval→fix loop, safe mutations, plan audit). Works alongside this MCP
server — the skills tell the agent how to choose between tools and
when to confirm destructive ones.

Source + docs: https://github.com/openbat-dev/agent-skills.

## See also

- [`@openbat/cli`](../cli/README.md) — same surface as a CLI for
  humans / scripts.
- [`@openbat/sdk`](../sdk/README.md) — capture conversations from your
  app (uses the ingest key only).
- [`lib/openbat-tools/`](../../lib/openbat-tools/README.md) — the
  registry that powers every MCP tool + CLI command + v1 route.
- [Agent skill bundle](https://github.com/openbat-dev/agent-skills) —
  procedural knowledge for AI agents (`npx skills add openbat-dev/agent-skills`).
- [A-Z test guide](../../docs/agent-surface-testing.md) — clone the
  repo and exercise every key kind, CLI, MCP, SDK in ~30 minutes.
