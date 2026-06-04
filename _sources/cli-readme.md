# @openbat/cli

Command-line tool for managing OpenBat chatbots end-to-end — read
analytics + conversations, pull daily eval digests (`review`), manage the
live system prompt (`prompts`), manage settings + keys + webhooks + workflows
+ reports, run experiments, and help install the SDK in a target app.
All commands operate on one **pinned chatbot** (`openbat use <id>`).

> **Companion docs**: [`@openbat/mcp`](../mcp/README.md) (same surface
> over MCP), [`lib/openbat-tools/`](../../lib/openbat-tools/README.md)
> (tool registry that powers both), and the
> [A-Z test guide](../../docs/agent-surface-testing.md).

## Install

```bash
npm i -g @openbat/cli
# or run on demand without installing:
npx @openbat/cli --help
```

---

## Authentication — four key kinds

The CLI accepts any read-capable OpenBat key. Pick the smallest scope
that works:

| Prefix | Kind | Scope | What you can do |
|---|---|---|---|
| `ob_read_*` | read | one chatbot, **read-only** | Listing, analytics, conversations, export |
| `ob_admin_*` | admin | one chatbot, **read+write** | All of read, plus webhooks / workflows / reports / settings / mint read keys |
| `ob_pat_*` | PAT | one user across multiple chatbots and orgs | All of admin, plus `chatbots create/delete`, `org`, mint admin keys, multi-chatbot inventory |
| `ob_live_*` | ingest | (rejected by the CLI) | SDK-only — capture endpoint. Never use here. |

PATs also carry a sub-scope on the row (`read` or `admin`). A read-scope
PAT can list across all your chatbots but mutate nothing.

Generate keys in the dashboard:
- **Read key** → `Settings → API Keys → Generate Read key`
- **Admin key** → `Settings → API Keys → Generate Admin key`
- **PAT** → `Settings → Personal Access Tokens`

Each plaintext is shown exactly once.

### Save the key

```bash
# Recommended — stdin keeps the plaintext out of shell history:
echo "ob_pat_..." | openbat config set-key --from-stdin
```

Stored at `~/.openbatrc` with mode `0600`. The CLI refuses to load if
the perms are looser than that.

**Auth resolution order** (each falls through to the next):

1. `--api-key <key>` flag — convenient but leaks into shell history;
   discouraged.
2. `$OPENBAT_API_KEY` env var — best for CI.
3. `~/.openbatrc` — persistent local default.

If you accidentally try to set an ingest key (`ob_live_*`), the CLI
rejects it with a helpful error.

---

## Pin to one chatbot (active-chatbot scope)

`ob_read_*` / `ob_admin_*` keys are already scoped to one chatbot server-side.
A `ob_pat_*` reaches many — pin one so every command stays on it:

```bash
openbat use <id|name>     # persists ~/.openbatrc.activeChatbotId
openbat use               # no arg → shows the current pin + reachable options
```

Once pinned, every data command (`conversations`, `analytics`, `review`,
`prompts`, …) targets that chatbot and prints a `→ chatbot: <name> (<id>)`
banner to **stderr** so scope is never in doubt (and `--json | jq` stays
clean). Active-chatbot resolution order: `--chatbot <id|name>` flag →
`$OPENBAT_CHATBOT_ID` → `~/.openbatrc`. The MCP server reads the same pin and
**hard-locks** to it (see [`@openbat/mcp`](../mcp/README.md)).

---

## Command tree

```
openbat
├── config
│   ├── set-key            Store / replace the key in ~/.openbatrc
│   ├── set-url <baseUrl>  Override the API base URL
│   ├── show               Print the resolved config (key prefix + active chatbot)
│   ├── use-chatbot <id|name>  Pin the active chatbot (persists to ~/.openbatrc)
│   └── clear-chatbot     Forget the pinned chatbot
│
├── use [id|name]                                             [any kind]
│   └── Pin the active chatbot (shortcut for `config use-chatbot`).
│       Omit the arg to print the current pin + the reachable list.
│
├── auth                                                      [any kind]
│   └── whoami             Show kind, chatbots in scope, orgs (PAT only)
│       (audit history: query api_audit_log in Supabase Studio — no CLI subcommand yet)
│
├── org                                                       [pat]
│   ├── list                                                  List user's orgs
│   ├── show                                                  Active org + members
│   ├── rename --id ORG --name "..."                          Owner only
│   ├── members list --id ORG
│   ├── members invite --id ORG --email --role member|admin
│   ├── members set-role --id ORG --member M --role admin|member
│   ├── members remove --id ORG --member M
│   └── invitations list --id ORG
│
├── chatbots                                                  [any kind]
│   ├── list                                                  Every chatbot in scope
│   ├── create --name --website [--docs-url] [--mcp-url]      [pat] mint chatbot + ingest key
│   └── delete <id>                                           [admin/pat] cascade delete
│
├── chatbot (legacy alias)
│   └── info                                                  [any kind] current chatbot row
│
├── conversations                                             [any kind]
│   ├── list [--days N] [--from ISO] [--to ISO] [--limit N] [--synthetic|--include-synthetic]
│   │       Organic-only by default; --synthetic = only probes, --include-synthetic = both
│   ├── show <id>             Messages + ALL analyses (issues/outcomes/flags/intents + reasoning)
│   └── await <id> [--timeout 90] [--message ID]
│           Block until the conversation's messages are fully analyzed. Accepts an
│           internal id OR a probe's obprobe_ id. Exit 0 when done, 2 on timeout.
│
├── probe <message> [--adapter PATH] [--timeout 90] [--no-wait]   [any kind]
│   └── Send a synthetic test query to YOUR chatbot (captured as kind=probe via a
│       reserved obprobe_ id), wait for analysis, print the verdict. With an
│       openbat.probe.json adapter it drives the chatbot for you; without one it
│       prints the conversationId + instructions so the agent issues the call.
│
├── eval                                                       [any kind]
│   ├── run --suite FILE [--adapter PATH] [--candidate VERSIONID] [--timeout 90] [--out FILE]
│   │       Probe each suite item, await, score against assertions, write a result file.
│   │       Suite: .json {items:[{id,question,expect?}]} or one-question-per-line .txt.
│   └── diff <runA.json> <runB.json>   Regression diff between two runs (exit 1 on regression)
│
├── optimize [--since 24h]                                     [any kind]
│   └── One-shot read-only diagnostic: organic review + active prompt + analysis defs
│       + a suggested probe plan. Bootstraps the eval loop in one command.
│
├── review [--since 45m|6h|7d]                                [any kind]
│   └── Daily eval digest: outcome/sentiment deltas + top issues/flags/intents
│       with representative conversation pointers. Default window 24h.
│
├── users                                                     [any kind]
│   └── list --chatbot ID [--days] [--search]                 External users + health
│
├── settings                                                  [admin or pat]
│   ├── update --chatbot ID [--description] [--website-url] [--language]
│   └── keys
│       ├── list-admin --chatbot ID
│       ├── rotate-ingest --chatbot ID                        New ob_live_* (shown once)
│       ├── generate-read --chatbot ID                        New ob_read_* (shown once)
│       ├── generate-admin --chatbot ID --name N [--expires-in-days]  [pat] new ob_admin_*
│       └── revoke-admin --chatbot ID --key KEYID             [pat] revoke
│
├── webhooks                                                  [admin or pat]
│   ├── list --chatbot ID
│   ├── create --chatbot ID --name --url --type discord|slack|custom    Returns signing secret (once)
│   └── delete --chatbot ID --webhook WHID
│
├── workflows                                                 [admin or pat]
│   ├── list --chatbot ID
│   └── create --chatbot ID --name --template T --trigger-value V --webhook WHID [--message TPL]
│       Templates: flag-to-webhook | outcome-to-webhook | sentiment-drop-to-webhook
│
├── reports                                                   [admin or pat]
│   ├── list --chatbot ID
│   └── create --chatbot ID [--name "..."]                    Returns org-private dashboard URL
│
├── prompts                                                   manage the LIVE published prompt
│   ├── list                                                  [any kind] versions + active + kill-switch
│   ├── publish --file PATH | --text "..."                    [admin/pat] create a version + set it LIVE
│   ├── create-draft --file PATH | --text "..."               [admin/pat] create a version WITHOUT activating (probe it, then activate)
│   ├── activate <versionId>                                  [admin/pat] roll back/forward to a version
│   └── kill-switch --on | --off                              [admin/pat] emergency fallback toggle
│
├── analysis                                                  [admin or pat]
│   ├── list --chatbot ID [--type] [--pending]
│   └── add --chatbot ID --type intent|flag|assistant_outcome|assistant_issue
│            --name SLUG --display-name "..." --description "..."
│
├── analytics                                                 [any kind]
│   ├── overview
│   └── sentiment [--days N]
│
├── export --format json|csv [--out FILE]                     [any kind] streaming export
│
└── sdk                                                       [any kind]
    ├── install-instructions [--framework next|node|vercel-ai-sdk] [--chatbot ID]
    └── verify --chatbot ID [--timeout N]                     Polls until first event
```

Every command supports `--json` for raw output (default for non-TTY
stdout, so piping into `jq` always works).

---

## Write commands — what to expect

Mutating commands follow a consistent output convention so scripts
and humans can both consume them cleanly:

- **Plaintext secrets go to stderr**, inside a "shown ONCE" banner:

  ```
  ────────────────────────────────────────────────────────────
    Webhook signing secret (shown ONCE — store this now)

    whsec_abcdef…
  ────────────────────────────────────────────────────────────
  ```

- **Structured response goes to stdout** without the plaintext, so
  `... | jq` keeps working:

  ```bash
  openbat webhooks create --chatbot $CB --name foo --url ... --type slack > webhook.json
  jq .id webhook.json
  ```

- **Errors go to stderr with a non-zero exit code.** API key plaintext
  is automatically redacted from any error message (`ob_admin_<16 chars>…<hidden>`).

- **HTTP 401 vs 403**: a 401 means "key invalid / expired / wrong kind
  for this endpoint" — usually fixed by `openbat auth whoami` + a fresh
  key. A 403 means "key valid but lacks permission" — e.g. a read-scope
  PAT trying to mutate, or a member trying to do an owner-only action.

- **HTTP 429** includes a `Retry-After` header. The CLI surfaces it in
  the error message.

---

## Quickstart — chatbot zero to first event

End-to-end in under 5 minutes. The full A-Z (including SDK install in a
real Next.js app) lives in
[`docs/agent-surface-testing.md`](../../docs/agent-surface-testing.md).

```bash
# 0. Configure a PAT (you mint this in the dashboard).
echo "ob_pat_..." | openbat config set-key --from-stdin

# 1. Verify scope.
openbat auth whoami

# 2. Create a chatbot.
openbat chatbots create --name "My Bot" --website https://example.com
#   stderr: Ingest API key (shown ONCE)
#   stdout: { chatbot: { id, ... }, dashboardUrl }
CB=<chatbot id from stdout>

# 3. Mint an admin key so we can manage it without the PAT.
openbat settings keys generate-admin --chatbot $CB --name "dev" --expires-in-days 30
#   stderr: ob_admin_... (shown ONCE)

# 4. Add a webhook + a workflow that fires it on a flag.
openbat webhooks create --chatbot $CB --name "ops" \
  --url https://hooks.slack.com/services/T.../B.../X --type slack
#   stdout: { id: WH_ID, ... }

openbat analysis add --chatbot $CB --type flag --name billing_issue \
  --display-name "Billing Issue" --description "Customer raises a billing concern"

openbat workflows create --chatbot $CB \
  --name "billing → slack" \
  --template flag-to-webhook \
  --trigger-value billing_issue \
  --webhook $WH_ID

# 5. Help an agent install the SDK in a target app.
openbat sdk install-instructions --framework next --chatbot $CB
# Markdown to stdout — agent (or you) follows the steps.

# 6. After SDK is wired up + a real chat sent, verify ingestion:
openbat sdk verify --chatbot $CB --timeout 60
# Exits 0 on first event, 2 on timeout.

# 7. Read your data.
openbat conversations list --days 7
openbat analytics overview
```

---

## The closed eval loop (probe → analyze → fix → re-probe)

The flagship workflow: an agent with your OpenBat key improves your chatbot by
**sending test queries, reading OpenBat's analysis, fixing the chatbot, and
re-testing** — a closed loop. OpenBat never calls your chatbot (it can't reach
it); the agent drives the chatbot and OpenBat owns the *eval leg*: synthetic
isolation, deterministic await, and the verdict.

```bash
# One command to diagnose what real users hit (probe-clean — excludes synthetic):
openbat optimize

# Send a synthetic test query. With an adapter it drives the chatbot for you:
cat > openbat.probe.json <<'JSON'
{ "url": "http://localhost:3000/api/chat", "method": "POST",
  "headers": { "content-type": "application/json" },
  "body": { "conversationId": "{{conversationId}}",
            "messages": [{ "role": "user", "content": "{{message}}" }] } }
JSON
openbat probe "how do I get a refund?"      # captures kind=probe, awaits, prints verdict

# Or run a whole suite + diff against a prior run to catch regressions after a fix:
openbat eval run --suite golden.json --out before.json
#   …apply your prompt/tool/retrieval fix, then:
openbat eval run --suite golden.json --out after.json
openbat eval diff before.json after.json     # exit 1 if anything regressed
```

**Synthetic isolation.** Probe/eval traffic is captured as `kind=probe` (the
SDK forwards a reserved `obprobe_` conversationId, or you pass `kind:"probe"`
explicitly). It is **excluded from organic `review`, the dashboard, and
analytics** so your test queries never skew real metrics. See it with
`openbat conversations list --synthetic`.

**Candidate prompts without shipping.** Stage a fix as a draft
(`openbat prompts create-draft --file new-prompt.txt`), probe the chatbot
against that version (the SDK's `versionOverride` / a `{{candidate}}` adapter
field), and only `openbat prompts activate <versionId>` once the eval passes.

The whole loop is also exposed over MCP (`openbat_probe`,
`openbat_await_analysis`, `openbat_optimize_context`, …) — see
[`@openbat/mcp`](../mcp/README.md).

## Override the API base URL

```bash
openbat config set-url https://staging.openbat.dev
# or per-invocation:
openbat --base-url http://localhost:3000 auth whoami
# or via env:
OPENBAT_BASE_URL=http://localhost:3000 openbat auth whoami
```

The CLI **refuses non-HTTPS base URLs** unless they point at `localhost`
or `127.0.0.1`. There is no `--insecure` escape hatch.

---

## Security properties

- API key plaintext never lands in any error message — auto-redacted to
  `ob_<kind>_<first 16>…<hidden>`.
- HTTPS-only base URL (localhost exception only).
- `~/.openbatrc` enforced at `mode 0600`; the loader refuses looser perms.
- Mint commands print plaintext to stderr only, with a "shown ONCE"
  banner. Pipe stderr to `/dev/null` if you don't want it on screen
  (you'll lose the secret).
- Every authenticated call lands in `api_audit_log` server-side
  (migration 036) — operators can answer "who did what when" via
  Supabase Studio.

## Rate limits

Per-tool buckets keyed by credential. The strict ones to know about:

| Operation | Limit |
|---|---|
| Create chatbot | 5 per hour per PAT |
| Mint or rotate any key | 10 per hour per credential |
| Create backtest | 10 per hour per PAT |
| Invite org member | 20 per hour per PAT |
| Chat with an AI report | 30 per minute per credential |
| Daily review digest (`review`) | 30 per minute per credential |
| Publish prompt | 20 per hour per credential |
| Activate prompt / toggle kill switch | 30 per hour per credential |
| Generic write | 60 per minute per credential |
| Generic read | 600 per minute per credential |
| Export | 30 per hour per credential |

429 responses include `Retry-After` (seconds).

---

## Pre-loaded context for AI assistants

If you're an AI agent (or driving one) and you'd like the procedural
knowledge for using this CLI delivered straight into your context,
install the OpenBat agent skill bundle:

```bash
npx skills add openbat-dev/agent-skills
```

Drops the `SKILL.md` bundle into your project's `.claude/skills/` (or the
equivalent for Cursor / Copilot / Gemini CLI / Codex / OpenCode / Amp).
The bundle covers chatbot onboarding, key management, webhooks,
workflows, AI reports, SDK install, the daily eval→fix loop
(`openbat-optimize`), and safety patterns — written specifically for the
four-kind auth ladder this CLI exposes.

Source + docs: https://github.com/openbat-dev/agent-skills.

## See also

- [`@openbat/mcp`](../mcp/README.md) — the same surface to Claude /
  Cursor / any MCP client.
- [`@openbat/sdk`](../sdk/README.md) — capture conversations from your
  app (uses the ingest key only).
- [`lib/openbat-tools/`](../../lib/openbat-tools/README.md) — the
  registry that powers every CLI command + MCP tool + v1 route.
- [Agent skill bundle](https://github.com/openbat-dev/agent-skills) —
  procedural knowledge for AI agents (`npx skills add openbat-dev/agent-skills`).
- [A-Z test guide](../../docs/agent-surface-testing.md) — clone the
  repo and exercise every key kind, CLI, MCP, SDK in ~30 minutes.
