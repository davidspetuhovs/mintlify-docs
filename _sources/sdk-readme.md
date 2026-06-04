# @openbat/sdk

TypeScript SDK for capturing AI chatbot conversations with [OpenBat](https://openbat.dev). Record messages, enrich with user/org context, and get AI-powered analysis — sentiment, intent detection, topic classification, quality scoring, behavioral flags, and more — with zero latency impact on your app.

## Installation

```bash
npm install @openbat/sdk
```

## Quick Start

```typescript
import { OpenBat } from "@openbat/sdk";

const client = new OpenBat({
  apiKey: process.env.OPENBAT_API_KEY,
});

await client.recordMessages({
  conversationId: "session-abc-123",
  messages: [
    { role: "user", content: "How do I reset my password?" },
    { role: "assistant", content: "Go to Settings > Security > Reset Password." },
  ],
});
```

That's it. Messages are sent asynchronously — errors are logged to console, never thrown.

---

## Configuration

### Constructor Options

```typescript
const client = new OpenBat({
  apiKey: "ob_live_...",       // Required (or set OPENBAT_API_KEY env var)
  baseUrl: "https://...",      // Optional, defaults to https://openbat.dev
  enabled: true,               // Optional, defaults to true

  // Optional. Wire this up to receive prompt updates pushed back from OpenBat
  // through the existing capture response — no polling, no extra fetches.
  // See "DB-Backed System Prompts" below.
  onPromptStateChange: async (state) => { /* write `state` to your DB */ },
});
```

### Environment Variables

| Variable | Purpose | Default |
|----------|---------|---------|
| `OPENBAT_API_KEY` | API key (used if not passed in constructor) | — |
| `OPENBAT_BASE_URL` | Override the capture endpoint base URL | `https://openbat.dev` |
| `OPENBAT_ENABLED` | Set to `"false"` or `"0"` to disable | `"true"` |

Constructor values take precedence over environment variables.

---

## Integration Guides

### Vercel AI SDK — `withOpenBat` Wrapper

The simplest integration. Wrap your `streamText` response and you're done.

```typescript
// app/api/chat/route.ts
import { streamText } from "ai";
import { openai } from "@ai-sdk/openai";
import { withOpenBat } from "@openbat/sdk";

export async function POST(req: Request) {
  const { messages } = await req.json();

  const result = streamText({
    model: openai("gpt-4o"),
    messages,
  });

  return withOpenBat(result.toDataStreamResponse(), {
    messages,
    conversationId: "session-abc-123", // optional, auto-generated UUID if omitted
    apiKey: process.env.OPENBAT_API_KEY,
    user: { id: "user-42", email: "jane@acme.com" },
  });
}
```

`withOpenBat` returns the original `Response` unchanged — zero interference with streaming.

### Vercel AI SDK — `onFinish` Pattern

For more control, record messages in the `onFinish` callback. This lets you capture the assistant's final response text and send only new messages (avoiding re-ingesting history on every turn).

This pattern is also the **only way** to capture tool calls and reasoning — the `withOpenBat` wrapper receives the final `Response` and cannot see tool calls. If your chatbot uses tools, use this pattern and pass them via the `tools` field so OpenBat can verify data-bearing claims against real tool output instead of flagging them as hallucinations.

```typescript
// app/api/chat/route.ts
import { streamText, UIMessage, convertToModelMessages } from "ai";
import { openai } from "@ai-sdk/openai";
import { OpenBat } from "@openbat/sdk";

const client = new OpenBat(); // reads OPENBAT_API_KEY from env

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json();

  // Forward client headers so OpenBat captures real IP/User-Agent
  const headers = Object.fromEntries(req.headers.entries());

  const result = streamText({
    model: openai("gpt-4o"),
    messages: await convertToModelMessages(messages),
    tools: {
      // your tools here
    },
    onFinish: async ({ text, toolCalls, toolResults, reasoningText }) => {
      // Extract last user message from UIMessage parts
      const lastUserMessage = [...messages]
        .reverse()
        .find((m) => m.role === "user");

      const lastUserContent =
        lastUserMessage?.parts
          ?.filter((p): p is { type: "text"; text: string } => p.type === "text")
          .map((p) => p.text)
          .join("") ?? "";

      // Map AI SDK tool calls to OpenBat's shape.
      // Pairing by array index works for `streamText` — toolResults[i] corresponds to toolCalls[i].
      const tools = toolCalls?.map((call, i) => ({
        name: call.toolName,
        input: call.input,
        output: toolResults?.[i]?.output,
      }));

      // Only send new messages — not the full history
      client.recordMessages({
        conversationId: "session-abc-123",
        user: { id: "user-42", email: "jane@acme.com" },
        headers: {
          "x-original-user-agent": headers["user-agent"] ?? "",
          "x-original-referer": headers["referer"] ?? "",
          "x-forwarded-for": headers["x-forwarded-for"] ?? headers["x-real-ip"] ?? "",
        },
        messages: [
          ...(lastUserContent
            ? [{ role: "user" as const, content: lastUserContent }]
            : []),
          {
            role: "assistant" as const,
            content: text,
            // Tool calls the model made before producing `text` (optional).
            // OpenBat's knowledge verifier uses these as ground truth for any
            // numbers, rankings, or entity data quoted in the response.
            ...(tools && tools.length > 0 ? { tools } : {}),
            // The model's internal reasoning/thinking, if available (optional).
            ...(reasoningText ? { reasoning: reasoningText } : {}),
          },
        ],
      });
    },
  });

  return result.toUIMessageStreamResponse();
}
```

### Direct API — Any Framework

Initialize the client once and call `recordMessages()` after each conversation turn.

```typescript
// lib/openbat.ts
import { OpenBat } from "@openbat/sdk";

export const openbat = new OpenBat({
  apiKey: process.env.OPENBAT_API_KEY,
});
```

```typescript
// wherever you handle chat
import { openbat } from "@/lib/openbat";

openbat.recordMessages({
  conversationId: session.id,
  messages: [
    { role: "user", content: userMessage },
    { role: "assistant", content: assistantResponse },
  ],
  user: { id: user.id, email: user.email },
});
```

### Express / Node.js

```typescript
import express from "express";
import { OpenBat } from "@openbat/sdk";

const app = express();
const openbat = new OpenBat(); // reads from OPENBAT_API_KEY env var

app.post("/api/chat", async (req, res) => {
  const { message, conversationId, userId } = req.body;

  // Your chat logic
  const reply = await getAIResponse(message);

  // Fire-and-forget — does not block the response
  openbat.recordMessages({
    conversationId,
    user: { id: userId },
    messages: [
      { role: "user", content: message },
      { role: "assistant", content: reply },
    ],
  });

  res.json({ reply });
});
```

### Raw HTTP — Any Language

If you're not using TypeScript, call the capture endpoint directly.

```bash
curl -X POST https://openbat.dev/api/v1/capture \
  -H "Content-Type: application/json" \
  -H "x-openbat-key: ob_live_your_api_key_here" \
  -d '{
    "conversationId": "session-abc-123",
    "messages": [
      { "role": "user", "content": "How do I reset my password?" },
      { "role": "assistant", "content": "Go to Settings > Security > Reset Password." }
    ],
    "user": { "id": "user-42", "email": "jane@acme.com" }
  }'
```

**Response:**

```json
{
  "ok": true,
  "conversationId": "uuid-...",
  "messagesStored": 2,
  "analysisQueued": 2
}
```

When you also send `systemPromptTemplate` in the request, the response includes a `prompt` field carrying the dashboard's current prompt state. See [DB-Backed System Prompts](#db-backed-system-prompts) for the full contract.

```json
{
  "ok": true,
  "conversationId": "uuid-...",
  "messagesStored": 2,
  "analysisQueued": 2,
  "prompt": {
    "currentVersionId": "9f3c...",
    "killSwitchOn": false,
    "isNew": true,
    "template": "You are a helpful assistant. ...",
    "publishedAt": "2026-05-05T12:00:00Z",
    "publishedBy": { "id": "uuid", "email": "alex@acme.com" }
  }
}
```

#### Python

```python
import requests

requests.post(
    "https://openbat.dev/api/v1/capture",
    headers={
        "Content-Type": "application/json",
        "x-openbat-key": "ob_live_your_api_key_here",
    },
    json={
        "conversationId": "session-abc-123",
        "messages": [
            {"role": "user", "content": "How do I reset my password?"},
            {"role": "assistant", "content": "Go to Settings > Security > Reset Password."},
        ],
        "user": {"id": "user-42"},
    },
)
```

---

## API Reference

### `OpenBat` Class

```typescript
import { OpenBat } from "@openbat/sdk";

const client = new OpenBat(config?: OpenBatConfig);
await client.recordMessages(input: RecordMessagesInput): Promise<void>;
```

**Throws** at construction if `enabled` is `true` and no API key is provided.

### `withOpenBat` Function

```typescript
import { withOpenBat } from "@openbat/sdk";

const response = withOpenBat(response: Response, options: WrapperOptions): Response;
```

Wraps a `Response` object, fires `recordMessages()` in the background, and returns the original response unchanged. Filters out `system` messages automatically. Generates a UUID for `conversationId` if not provided.

### Types

```typescript
interface OpenBatConfig {
  apiKey?: string;
  baseUrl?: string;
  enabled?: boolean;
  /**
   * Fired whenever OpenBat tells the SDK something it doesn't already know
   * about your prompt state — a new version, a kill-switch transition, or a
   * fresh active version id. See "DB-Backed System Prompts" for details.
   * Errors thrown inside the callback are caught + logged, never propagated.
   */
  onPromptStateChange?: (state: PromptState) => void | Promise<void>;
}

type PromptState =
  | {
      // Steady state — your submitted template hash matches the active version.
      currentVersionId: string | null;   // null if no published prompt yet
      killSwitchOn: boolean;
      isNew: false;
    }
  | {
      // Update — your submitted template hash differs from the active version.
      currentVersionId: string;
      killSwitchOn: boolean;
      isNew: true;
      template: string;
      publishedAt: string;               // ISO 8601
      publishedBy: { id: string; email: string };
    };

interface RecordMessagesInput {
  conversationId: string;
  kind?: "organic" | "probe";   // "probe" = synthetic eval traffic, excluded from organic analytics/review (default "organic"). The server also infers "probe" from a reserved `obprobe_` conversationId prefix.
  user?: OpenBatUser;
  organization?: OpenBatOrganization;
  session?: OpenBatSession;
  custom?: Record<string, string | number | boolean>;
  systemPromptTemplate?: string;  // Unrendered system prompt — enables versioning
  systemPromptVariables?: Record<string, string | number | boolean>;  // Resolved values for this call
  headers?: Record<string, string>;
  framework?: string;             // Optional integration hint, surfaced as the x-openbat-framework header (e.g. "vercel-ai-sdk")
  messages: Array<{
    role: "user" | "assistant" | "system";
    content: string;
    id?: string;             // External ID for deduplication
    sentAt?: Date;           // Timestamp (serialized to ISO string)
    tools?: OpenBatToolCall[]; // Tools the assistant called (assistant messages)
    reasoning?: string;      // The model's internal reasoning/thinking (assistant messages)
  }>;
}

interface OpenBatToolCall {
  name: string;      // Tool name, e.g. "getBrandMetrics"
  input?: unknown;   // Arguments passed to the tool (optional)
  output?: unknown;  // Result returned by the tool (optional)
}

interface OpenBatUser {
  id?: string;
  name?: string;
  email?: string;
  plan?: string;         // e.g. "pro", "enterprise"
  createdAt?: string;    // ISO datetime
  industry?: string;
  mrr?: number;          // Monthly recurring revenue in cents
}

interface OpenBatOrganization {
  id?: string;
  name?: string;
  plan?: string;
  mrr?: number;
  industry?: string;
}

interface OpenBatSession {
  id?: string;
  pageUrl?: string;
  referrer?: string;
  device?: "mobile" | "desktop" | "tablet";
  country?: string;     // ISO country code
}

interface WrapperOptions {
  apiKey?: string;
  baseUrl?: string;
  messages: Array<{ role: string; content: unknown }>;
  conversationId?: string;
  user?: OpenBatUser;
  organization?: OpenBatOrganization;
  session?: OpenBatSession;
  custom?: Record<string, string | number | boolean>;
}
```

---

## Enriching Context

Attach business context to conversations for richer analytics in the dashboard.

```typescript
client.recordMessages({
  conversationId: "session-abc-123",
  messages: [...],

  // Who is chatting
  user: {
    id: "user-42",
    name: "Jane Smith",
    email: "jane@acme.com",
    plan: "enterprise",
    industry: "fintech",
    mrr: 49900,  // $499.00
  },

  // Their organization
  organization: {
    id: "org-7",
    name: "Acme Corp",
    plan: "enterprise",
    mrr: 249900,
    industry: "fintech",
  },

  // Session context
  session: {
    id: "sess-xyz",
    pageUrl: "https://app.acme.com/support",
    referrer: "https://google.com",
    device: "desktop",
    country: "US",
  },

  // Arbitrary key-value pairs
  custom: {
    feature: "billing",
    chatbotVersion: "2.1",
    isTrialUser: true,
  },
});
```

All context fields are optional. Send what you have — even just `user.id` helps segment conversations in the dashboard.

---

## System Prompt Versioning

Pass the unrendered system prompt your chatbot is running under to OpenBat. The capture endpoint hashes it (SHA-256 of exact bytes) and stores each unique template once per chatbot. Every captured message is then linked to the prompt version active at the time it was sent — so you can correlate quality issues, tag rates, or sentiment shifts back to the specific prompt that produced them, and review your prompt history in the dashboard.

Two fields, both optional, both at the root of `recordMessages()`:

```typescript
client.recordMessages({
  conversationId: "session-abc-123",
  messages: [...],

  // The TEMPLATE — pass it before any variable interpolation, exactly as it
  // lives in your source. OpenBat does NOT parse it: any syntax works
  // (mustache, JS template literals, f-strings, etc.).
  systemPromptTemplate:
    "You are a {{role}} assistant for {{company}}. Be concise and {{tone}}.",

  // Optional: the resolved values for THIS call, stored verbatim alongside
  // each message. Use this if you want to investigate variable-conditional
  // behaviour later.
  systemPromptVariables: {
    role: "support",
    company: "Acme",
    tone: "warm",
  },
});
```

### Wiring it into an AI SDK call

Define the template once, render for the LLM call, pass both to OpenBat:

```typescript
const SYSTEM_TEMPLATE =
  "You are a {{role}} assistant for {{company}}. Be concise and {{tone}}.";

const variables = { role: "support", company: "Acme", tone: "warm" };

const renderedSystem = SYSTEM_TEMPLATE
  .replace("{{role}}", variables.role)
  .replace("{{company}}", variables.company)
  .replace("{{tone}}", variables.tone);

const result = streamText({
  model: openai("gpt-4o"),
  system: renderedSystem,
  messages,
  onFinish: async ({ text }) => {
    await client.recordMessages({
      conversationId: "session-abc-123",
      systemPromptTemplate: SYSTEM_TEMPLATE,  // unrendered
      systemPromptVariables: variables,
      messages: [
        { role: "user", content: lastUserContent },
        { role: "assistant", content: text },
      ],
    });
  },
});
```

### How identity works

Identity is **byte-exact**. SHA-256 of the UTF-8 bytes of `systemPromptTemplate`. No whitespace normalization, no case-folding, no punctuation stripping.

- Pass the same template twice → same version row.
- Trim a trailing space → new version row.
- Revert to a previous template's exact bytes → new messages re-link to the **original** version row. No duplicate version is created and the dashboard shows it as a single entity.

### Why pass the template, not the rendered prompt

If you pre-interpolate variables (e.g. RAG context, user profile, current date) into the prompt before sending to OpenBat, every call would land in its own version bucket and the dashboard couldn't aggregate metrics across them. Keeping `systemPromptTemplate` stable and passing values through `systemPromptVariables` keeps your version history meaningful.

### What you see in the dashboard

The chatbot's **System Prompt** page shows:

- The currently active version (the one most recently linked to a message).
- The full version history with first-seen timestamps and message counts.
- Inline diffs between any two versions.

> The dashboard is now **read/write** — you can edit and publish prompts directly. Your hardcoded `fallback` stays the safety net. See [Remote-Controlled System Prompts](#remote-controlled-system-prompts).

### What happens if you don't pass it

Messages still capture as normal, but with no prompt-version link (`prompt_version_id = NULL`). The Settings tab shows an empty state with the SDK snippet to wire up. No errors, no warnings, no breaking change to existing integrations.

---

## DB-Backed System Prompts

> **Recommended path** for production setups with a database. For most chatbots, prefer this over the runtime-fetch alternative ([Remote-Controlled System Prompts](#remote-controlled-system-prompts)) further down — your app stays decoupled from OpenBat at request time.

OpenBat owns the dashboard for editing your prompt. Your **own database** stores the active version your app reads at request time. OpenBat pushes new versions back to you in the response of your existing capture calls — no polling, no extra fetches on the request path, no runtime dependency on OpenBat being reachable.

The mental model: **single source of truth = your DB**. The OpenBat dashboard is the editor; your DB is the warehouse; your app is the reader.

### How it works

```
1. Your app reads its system prompt from your DB
2. Your app calls the LLM with that prompt
3. Your app calls openbat.recordMessages(...) — passing the prompt template
4. OpenBat hashes the template, compares to the dashboard's active version
5. If different, the response includes the new template + metadata
6. The SDK fires your onPromptStateChange callback with the new state
7. Your code writes it into your DB
8. The next request reads the new prompt from your DB
```

Zero added network calls. Zero polling. Self-healing — every conversation re-checks freshness against the dashboard.

### Wiring up the callback

```typescript
import { OpenBat } from "@openbat/sdk";

const HARDCODED_FALLBACK = "You are a helpful assistant. Be concise.";

const openbat = new OpenBat({
  apiKey: process.env.OPENBAT_API_KEY,
  onPromptStateChange: async (state) => {
    // Your code. OpenBat does NOT know what database you use.
    // Translate `state` into INSERT/UPSERT calls against your storage.
    if (state.isNew) {
      await yourDb.insertPrompt({
        versionId: state.currentVersionId,
        template: state.template,
        publishedAt: state.publishedAt,
        publishedByEmail: state.publishedBy.email,
      });
    }
    await yourDb.upsertSettings({
      killSwitchOn: state.killSwitchOn,
      currentVersionId: state.currentVersionId,
    });
  },
});
```

The callback fires whenever OpenBat tells your SDK something it doesn't already know — a new prompt version, a kill-switch transition, or a fresh `currentVersionId`. It runs from inside `recordMessages()` regardless of whether you `await` the outer call, so it works with `withOpenBat()`, fire-and-forget patterns, and standard awaited calls equally.

If the callback throws, the SDK catches and logs to `console.error` — it never propagates the error up to your `recordMessages()` call.

### Response contract

Every `recordMessages()` response (and the matching JSON for `POST /api/v1/capture`) includes a `prompt` field whenever you sent `systemPromptTemplate` in the request:

```typescript
type PromptState =
  | {
      // Steady state — what you have matches what OpenBat has.
      currentVersionId: string | null;   // null if no published prompt yet
      killSwitchOn: boolean;
      isNew: false;
    }
  | {
      // Update — your submitted template hash differs from the active version.
      currentVersionId: string;
      killSwitchOn: boolean;
      isNew: true;
      template: string;                  // the new prompt
      publishedAt: string;               // ISO 8601
      publishedBy: { id: string; email: string };
    };
```

| Field | When present | Purpose |
|---|---|---|
| `currentVersionId` | always | what OpenBat thinks is active right now (or `null`) |
| `killSwitchOn` | always | when `true`, your app must serve the hardcoded fallback regardless of DB contents |
| `isNew` | always | `true` iff your submitted `systemPromptTemplate` doesn't match the active version |
| `template` | only when `isNew` | the new prompt text |
| `publishedAt` | only when `isNew` | ISO 8601 timestamp |
| `publishedBy` | only when `isNew` | who on the operator's team published — for your audit log |

If you don't send `systemPromptTemplate` in your capture call, the `prompt` field is omitted entirely and the callback does not fire.

### Reading the active prompt at request time

You write this — OpenBat doesn't ship a read helper because it doesn't know your stack. The shape:

```typescript
async function getActiveSystemPrompt(): Promise<string> {
  const settings = await yourDb.getSettings();
  if (settings?.killSwitchOn) return HARDCODED_FALLBACK;

  const latest = await yourDb.getLatestPrompt();
  return latest?.template ?? HARDCODED_FALLBACK;
}
```

Three rules:

1. **Kill switch always wins.** If on, return the hardcoded fallback.
2. **Empty DB = bootstrap.** Cold deploy, never received a prompt yet → return the fallback.
3. **Otherwise** return whatever's most recent in your DB.

### The bootstrap fallback

You keep `HARDCODED_FALLBACK` as a constant in your code. It runs:

- On the very first request after deploy (before the first capture round-trip populates your DB)
- During an OpenBat outage if your DB ever gets wiped
- When the kill switch is on

It's not a duplicate of your live prompt — it's the disaster-recovery snapshot. Treat it like the prompt's last line of defence. Anyone reading your repo can still see what your chatbot says.

### Recommended schema (translate to your stack)

OpenBat does not prescribe a schema. The data shape you're storing is roughly:

```
prompts (
  version_id          UUID PRIMARY KEY,
  template            TEXT NOT NULL,
  published_at        TIMESTAMP NOT NULL,
  published_by_email  TEXT,
  inserted_at         TIMESTAMP NOT NULL DEFAULT now()
)

settings (
  chatbot_id          PRIMARY KEY  -- string or singleton
  kill_switch_on      BOOLEAN NOT NULL,
  current_version_id  UUID,        -- what OpenBat last told us is active
  updated_at          TIMESTAMP NOT NULL
)
```

Critical: use `ON CONFLICT (version_id) DO NOTHING` (or your DB's equivalent) on the prompts table. Multiple SDK instances may receive the same update concurrently across cold starts — duplicate writes should be silent no-ops, not errors. The SDK does NOT dedupe in process memory; your DB is the dedupe layer.

### End-to-end example

```typescript
import { streamText } from "ai";
import { openai } from "@ai-sdk/openai";
import { OpenBat } from "@openbat/sdk";

const HARDCODED_FALLBACK = "You are a helpful assistant. Be concise.";

const openbat = new OpenBat({
  apiKey: process.env.OPENBAT_API_KEY,
  onPromptStateChange: async (state) => {
    if (state.isNew) {
      await yourDb.insertPrompt({
        versionId: state.currentVersionId,
        template: state.template,
        publishedAt: state.publishedAt,
        publishedByEmail: state.publishedBy.email,
      });
    }
    await yourDb.upsertSettings({
      killSwitchOn: state.killSwitchOn,
      currentVersionId: state.currentVersionId,
    });
  },
});

async function getActiveSystemPrompt(): Promise<string> {
  const settings = await yourDb.getSettings();
  if (settings?.killSwitchOn) return HARDCODED_FALLBACK;
  const latest = await yourDb.getLatestPrompt();
  return latest?.template ?? HARDCODED_FALLBACK;
}

export async function POST(req: Request) {
  const { messages, conversationId } = await req.json();

  const systemPrompt = await getActiveSystemPrompt();

  const result = streamText({
    model: openai("gpt-4o"),
    system: systemPrompt,
    messages,
    onFinish: async ({ text }) => {
      // Pass back the prompt that was actually served. OpenBat compares it
      // against the active version and replies with an update if you're stale —
      // your callback fires automatically.
      await openbat.recordMessages({
        conversationId,
        systemPromptTemplate: systemPrompt,
        messages: [
          { role: "user", content: lastUserContent },
          { role: "assistant", content: text },
        ],
      });
    },
  });

  return result.toUIMessageStreamResponse();
}
```

### Cold-instance fan-out

The SDK tracks "what state did I last see" in process memory only — there is no shared state across SDK instances. Every cold instance fires the callback once on its first capture response. This is honest about the distributed-systems reality: your DB upsert is the dedupe layer (`ON CONFLICT DO NOTHING` for prompt versions, last-write-wins for the settings row). Don't be alarmed by callback fires across cold instances; they're bounded by your traffic shape.

### Detection

When you wire up `onPromptStateChange`, the SDK adds an `x-openbat-prompt-callback: configured` header to every capture call. OpenBat uses this to mark your chatbot as DB-Backed (Layer 6) Active in the integration tab — there's nothing for you to toggle.

### When the prompt field is omitted

The `prompt` field is omitted from the response — and the callback does not fire — when:

- You didn't send `systemPromptTemplate` in your capture call (you're on a non-prompt-aware integration tier).
- The chatbot's API key is invalid (you'll see a 401 instead).

### Versus runtime fetch

`onPromptStateChange` (this section) and [`getSystemPrompt`](#remote-controlled-system-prompts) (below) are two ways to consume dashboard-published prompts. They solve the same problem from opposite ends:

| | `onPromptStateChange` (DB-backed) | `getSystemPrompt` (runtime fetch) |
|---|---|---|
| Runtime source | Your own DB | OpenBat (with TTL cache + fallback) |
| Network dep at request time | None — local DB read | Yes — SDK calls OpenBat |
| Cold-start latency | Always fast (local read) | Up to 100ms then fallback |
| OpenBat outage | Your DB keeps serving forever | Stale cache then eventual fallback |
| Setup cost | Schema + write handler + read path | One SDK call |

**Use `onPromptStateChange`** if you have a database and want zero runtime dependency on OpenBat.

**Use `getSystemPrompt`** if you can't host a database (edge functions, browser-based agents, simple scripts) or if your prompt rarely changes and the convenience of a one-line setup outweighs the runtime dependency.

You can configure both, but it's unusual — the two paths will populate two different runtime sources. Pick one.

---

## Remote-Controlled System Prompts

> For most production setups, prefer [DB-Backed System Prompts](#db-backed-system-prompts) above. Use this path when you can't host a database or you need single-line setup.

Author and publish your chatbot's system prompt directly from the OpenBat dashboard. Iterate on a prompt — even a one-line tweak — without a redeploy. Roll back to a previous version in one click. Hit the kill switch during incidents to revert to your hardcoded fallback. The `fallback` you pass stays the safety net: if OpenBat is unreachable, the kill switch is on, or no prompt has been published, your chatbot keeps running on the prompt that lives in your code.

### Opt in with one line

```typescript
const { template: systemPrompt } = await client.getSystemPrompt({
  fallback: HARDCODED_SYSTEM_PROMPT,
});
```

Pass `systemPrompt` to your LLM. Adoption is opt-in by this single call — until you add it, your chatbot keeps using your hardcoded prompt and nothing changes.

### End-to-end with `streamText`

```typescript
import { streamText } from "ai";
import { openai } from "@ai-sdk/openai";
import { OpenBat } from "@openbat/sdk";

const client = new OpenBat();

const FALLBACK_TEMPLATE =
  "You are a {{role}} assistant for {{company}}. Be concise and {{tone}}.";

export async function POST(req: Request) {
  const { messages, conversationId } = await req.json();

  const variables = { role: "support", company: "Acme", tone: "warm" };

  const { template, source } = await client.getSystemPrompt({
    fallback: FALLBACK_TEMPLATE,
    conversationId,
  });

  const renderedSystem = template
    .replace("{{role}}", variables.role)
    .replace("{{company}}", variables.company)
    .replace("{{tone}}", variables.tone);

  const result = streamText({
    model: openai("gpt-4o"),
    system: renderedSystem,
    messages,
    onFinish: async ({ text }) => {
      await client.recordMessages({
        conversationId,
        // Pass the template the LLM actually saw (live or fallback) so
        // version history stays accurate.
        systemPromptTemplate: template,
        systemPromptVariables: variables,
        messages: [...],
      });
    },
  });

  return result.toUIMessageStreamResponse();
}
```

### Behaviour

`getSystemPrompt` returns `{ template, source }` and **never throws**. The `source` field tells you where the prompt came from:

| Situation | Returns | `source` |
|---|---|---|
| Cache hit (within 60s of last fetch) | cached template | `"cache"` |
| Cache miss, server reachable | live template | `"remote"` |
| Cache miss, cold-start, fetch exceeds `coldStartTimeoutMs` (default 100ms) | your fallback | `"fallback"` |
| OpenBat unreachable, prior cache exists | last-known-good (stale) | `"cache"` |
| OpenBat unreachable, no cache | your fallback | `"fallback"` |
| Kill switch ON in dashboard | your fallback | `"kill_switch"` |
| No published prompt for this chatbot | your fallback | `"fallback"` |

The first call after a cold start hits the network. Subsequent calls within 60s return synchronously from the in-memory cache. Stale entries refresh in the background while serving the existing value, so you never block on a refresh.

### Configuration

```typescript
await client.getSystemPrompt({
  fallback: "...",                   // required
  conversationId: "...",             // optional, plumbed for future A/B testing
  mode: "instant_fallback",          // optional — skips the cold-start fetch entirely
  coldStartTimeoutMs: 100,           // optional — default 100ms
  versionOverride: "...",            // optional — pin a specific (draft) version for probe/eval
});
```

- **`mode: "instant_fallback"`** — never block on the fetch; return fallback immediately on cold start. The fetch still runs in the background so subsequent calls return the live prompt. Use if you have extreme first-request latency requirements.
- **`coldStartTimeoutMs`** — only enforced before the cache is warm. Once a fetch has succeeded once, subsequent calls return synchronously from cache.
- **`versionOverride`** — fetch a SPECIFIC published version id instead of the live active prompt, bypassing the cache. Forward this from a probe/eval request (e.g. an `x-openbat-prompt-version` header your route reads) so an eval can run the chatbot against a **candidate draft** created with `openbat prompts create-draft` — without shipping it to production. The version must belong to this chatbot (server-enforced); the kill switch still applies; on any error you get your `fallback`.

### The fallback is sacred

Keep your hardcoded fallback up to date. It's what runs during an OpenBat outage, when the kill switch is on, or before the first fetch resolves. Treat it as your prompt's last line of defence — anyone reading your repo can still see what your chatbot says.

---

## Tool-Aware Verification

If your chatbot calls tools (database queries, API lookups, etc.) before answering, attach the tool calls to the assistant message. OpenBat's knowledge verifier uses them as ground truth when checking for hallucination.

**Why it matters.** Without tool context, a response like `"NeN holds the #1 position with a visibility score of 76.9"` looks suspicious — docs don't contain that number. The verifier would have to decide whether to flag it. **With** tool context, the verifier compares the quoted value against the actual tool output: if it matches, the claim is trusted; if it doesn't, it's flagged as hallucination with the tool output quoted as evidence. No more false positives on runtime data.

```typescript
client.recordMessages({
  conversationId: "session-abc-123",
  messages: [
    { role: "user", content: "Who has the highest visibility score?" },
    {
      role: "assistant",
      content: "NeN holds the #1 visibility position with a score of 76.9.",
      tools: [
        {
          name: "getBrandMetrics",
          input: {},
          output: {
            currentWeek: [
              { brand_name: "NeN", visibility_score: 76.9, brand_ranking: 1 },
              { brand_name: "Sorgenia", visibility_score: 75.1, brand_ranking: 2 },
            ],
          },
        },
      ],
      // Optional: the model's thinking before it answered.
      // Supported by reasoning-capable models (Claude with thinking, OpenAI o-series, etc.).
      reasoning: "I need to call getBrandMetrics to find the top brand by visibility score.",
    },
  ],
});
```

**Limits.** Up to 20 tools per message; the serialized `{tools, reasoning}` blob must be under 32 KB. Anything larger is rejected with `400 Bad Request`. Tools and reasoning are stored only for the verification step — they're not surfaced to end users.

**Capture only.** Only assistant messages use `tools` / `reasoning`. Fields on user or system messages are ignored.

---

## Message Deduplication

Set `id` on messages to prevent duplicates when re-sending conversation history.

```typescript
client.recordMessages({
  conversationId: "session-abc-123",
  messages: [
    { id: "msg-001", role: "user", content: "Hello" },         // stored on first call
    { id: "msg-002", role: "assistant", content: "Hi there!" }, // stored on first call
    { id: "msg-001", role: "user", content: "Hello" },         // skipped (duplicate)
    { id: "msg-003", role: "user", content: "Help me" },       // stored (new)
  ],
});
```

Messages with `id` are deduplicated per conversation. Messages without `id` are always inserted.

---

## Header Forwarding

When your SDK calls originate from a server-side route (e.g., Next.js API route), the capture endpoint sees your server's IP and User-Agent instead of the real user's. Forward the original headers to get accurate client metadata:

```typescript
// Inside your API route handler
const headers = Object.fromEntries(req.headers.entries());

client.recordMessages({
  conversationId: "session-abc-123",
  messages: [...],
  headers: {
    "x-original-user-agent": headers["user-agent"] ?? "",
    "x-original-referer": headers["referer"] ?? "",
    "x-forwarded-for": headers["x-forwarded-for"] ?? headers["x-real-ip"] ?? "",
  },
});
```

The capture endpoint automatically parses these headers to extract: IP address, browser, OS, device type, language, timezone, country, city, and region.

---

## Error Handling

The SDK is designed to be invisible — it never throws errors or blocks your application.

- `recordMessages()` catches all errors internally
- HTTP errors are logged: `OpenBat Error: HTTP 400 — ...`
- Network failures are logged: `OpenBat Error: Failed to record messages.`
- All errors go to `console.error` — they never propagate to your code

If you need to verify the SDK is working, check your browser/server console for error messages, or visit the OpenBat dashboard to confirm messages are arriving.

---

## Disabling the SDK

Disable the SDK in test or development environments:

```bash
# Environment variable
OPENBAT_ENABLED=false
```

```typescript
// Or in code
const client = new OpenBat({
  apiKey: "ob_live_...",
  enabled: process.env.NODE_ENV === "production",
});
```

When disabled, `recordMessages()` returns immediately without making any HTTP requests.

---

## API Limits

| Constraint | Limit |
|------------|-------|
| Request body size | 4 MB |
| Messages per request | 1–100 |
| Message content length | 1–32,000 characters |
| `conversationId` length | 1–256 characters |
| `message.id` length | max 256 characters |
| `user.email` | Must be a valid email, max 256 characters |
| `user.plan` / `organization.plan` | max 64 characters |
| `user.name` / `organization.name` | max 256 characters |
| `session.pageUrl` / `session.referrer` | max 2,048 characters |
| `custom` field values | `string`, `number`, or `boolean` only |
| `systemPromptTemplate` length | 1–64,000 characters |
| `systemPromptVariables` keys | max 100, key 1–256 characters |
| `systemPromptVariables` values | `string`, `number`, or `boolean` only |

Requests exceeding these limits receive a `400 Bad Request` response (logged to console, never thrown).

---

## Releasing a new SDK version

Internal-maintainer notes for shipping a new published version to npm.

1. Bump the version in `packages/sdk/package.json` (semver: minor for new methods, patch for bug fixes, major for breaking changes).
2. Add an entry to `packages/sdk/CHANGELOG.md` describing what changed and any migration notes.
3. From the repo root, run `npm run sdk:build` to produce the dist artifacts.
4. From `packages/sdk/`, run `npm publish --access public`. Requires npm login with publish rights to the `@openbat` scope.
5. Verify with `npm view @openbat/sdk version` — it should match the version you just bumped.
6. Tag the release in git: `git tag sdk-v<version> && git push --tags`.

Do not publish from a feature branch — merge to `main` first. The `dist/` folder is built fresh on each publish (it's `.gitignore`d in the repo).

---

## License

MIT
