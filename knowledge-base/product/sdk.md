# SDK

The OpenBat SDK is a lightweight TypeScript client that captures conversation data from your AI chatbot and sends it to OpenBat for analysis. It's designed to be fire-and-forget — it never blocks your response pipeline.

---

## Installation

```bash
npm install openbat
# or
yarn add openbat
# or
pnpm add openbat
```

---

## Quick Start

```typescript
import { OpenBat } from 'openbat';

const client = new OpenBat({
  apiKey: process.env.OPENBAT_API_KEY
});

// Call this after your chatbot generates a response
await client.recordMessages({
  conversationId: "conv_unique_id",
  messages: [
    { role: "user", content: "How do I reset my password?" },
    { role: "assistant", content: "You can reset your password by..." }
  ]
});
```

That's the minimal integration. Everything else is optional enrichment.

---

## Configuration

### Constructor

```typescript
const client = new OpenBat({
  apiKey?: string,      // defaults to OPENBAT_API_KEY env var
  baseUrl?: string,     // defaults to OPENBAT_BASE_URL or "https://app.openbat.dev"
  enabled?: boolean     // defaults to OPENBAT_ENABLED env var (true unless "false" or "0")
});
```

The `enabled` flag lets you disable OpenBat in test/CI environments without changing code:

```bash
# .env.test
OPENBAT_ENABLED=false
```

---

## Recording Messages

### `client.recordMessages(input)`

The main method. Sends conversation messages with optional metadata to OpenBat.

```typescript
await client.recordMessages({
  // Required
  conversationId: string,        // Your unique ID for this conversation

  // Messages (required, 1–100 per call)
  messages: Array<{
    role: "user" | "assistant" | "system",
    content: string,
    id?: string,      // External message ID (used for deduplication)
    sentAt?: Date     // When the message was sent
  }>,

  // User metadata (optional but highly recommended)
  user?: {
    id?: string,
    name?: string,
    email?: string,
    plan?: string,         // "free" | "pro" | "enterprise" | etc.
    createdAt?: Date,
    industry?: string,
    mrr?: number           // Monthly recurring revenue in dollars
  },

  // Organization metadata (optional)
  organization?: {
    id?: string,
    name?: string,
    plan?: string,
    mrr?: number,
    industry?: string
  },

  // Session metadata (optional)
  session?: {
    id?: string,
    pageUrl?: string,
    referrer?: string,
    device?: string,    // "desktop" | "mobile" | "tablet"
    country?: string
  },

  // Custom fields (optional — must match your chatbot's metadata schema)
  custom?: Record<string, string | number | boolean>,

  // Forward request headers (optional — for server-side use)
  headers?: Record<string, string>
});
```

**Returns:** `Promise<void>` — errors are caught and logged internally, never thrown.

---

## Enriching Your Data

The more metadata you provide, the more powerful your filtering and segmentation in the dashboard becomes. Here's a fully enriched call:

```typescript
await client.recordMessages({
  conversationId: `conv_${userId}_${sessionId}`,

  user: {
    id: user.id,
    name: user.fullName,
    email: user.email,
    plan: user.subscriptionPlan,   // "starter" | "pro" | "enterprise"
    createdAt: user.createdAt,
    industry: user.company?.industry,
    mrr: user.monthlyRevenue
  },

  organization: {
    id: user.organization.id,
    name: user.organization.name,
    plan: user.organization.plan,
    mrr: user.organization.monthlyRevenue,
    industry: user.organization.industry
  },

  session: {
    id: sessionId,
    pageUrl: req.headers['referer'],
    device: detectDevice(req.headers['user-agent']),
    country: req.headers['cf-ipcountry']   // Cloudflare header
  },

  custom: {
    trial_days_remaining: user.trialDaysLeft,
    feature_flags: user.activeFeatures.join(","),
    account_tier: user.accountTier
  },

  messages: conversationHistory
});
```

With this data, in the OpenBat dashboard you can filter conversations by plan, industry, MRR range, or any custom field.

---

## Message Deduplication

If you pass an `id` field on each message, OpenBat deduplicates on that ID. This means you can safely call `recordMessages` on every turn without worrying about inserting duplicate messages:

```typescript
// Safe to call on every AI response — duplicate message IDs are ignored
await client.recordMessages({
  conversationId: threadId,
  messages: allMessages.map(msg => ({
    role: msg.role,
    content: msg.content,
    id: msg.id,          // ← deduplication key
    sentAt: msg.createdAt
  }))
});
```

If no `id` is provided, OpenBat uses the message content + role + timestamp combination, but explicit IDs are more reliable.

---

## Vercel AI SDK Integration

OpenBat ships a `withOpenBat` wrapper specifically for use with the Vercel AI SDK's streaming response pattern:

```typescript
import { streamText } from 'ai';
import { withOpenBat } from 'openbat';

export async function POST(req: Request) {
  const { messages, conversationId, user } = await req.json();

  const result = streamText({
    model: yourModel,
    messages
  });

  // Wraps the stream response — captures messages in background, returns stream unchanged
  return withOpenBat(result.toUIMessageStreamResponse(), {
    conversationId,
    user,
    messages
  });
}
```

`withOpenBat` extracts user and assistant messages, calls `recordMessages` non-blocking in the background, and returns the response unchanged. Your streaming latency is unaffected.

---

## Server-Side Usage (Next.js Route Handler)

```typescript
// app/api/chat/route.ts
import { OpenBat } from 'openbat';

const bat = new OpenBat();

export async function POST(req: Request) {
  const { messages, metadata } = await req.json();

  // Generate your AI response
  const response = await generateResponse(messages);

  // Capture in background — doesn't block the response
  bat.recordMessages({
    conversationId: metadata.conversationId,
    user: metadata.user,
    organization: metadata.organization,
    messages: [
      ...messages,
      { role: "assistant", content: response.content }
    ],
    headers: Object.fromEntries(req.headers)  // Forward for geo/device detection
  });

  return Response.json({ content: response.content });
}
```

Pass `headers` from the incoming request to enable automatic geo and device detection from Cloudflare headers (`cf-ipcountry`, `cf-connecting-ip`, `user-agent`).

---

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `OPENBAT_API_KEY` | Your chatbot's API key (`ob_live_...`) | — (required if not in config) |
| `OPENBAT_BASE_URL` | API base URL | `https://app.openbat.dev` |
| `OPENBAT_ENABLED` | Set to `"false"` or `"0"` to disable | `true` |

---

## Getting Your API Key

1. Go to your chatbot's Settings page in the OpenBat dashboard
2. The API key prefix is shown in the General tab
3. If you've lost the full key, use **Rotate Key** to generate a new one (the full key is shown only at creation/rotation)
4. Copy the key into your `OPENBAT_API_KEY` environment variable

---

## Error Handling

The SDK is designed to be invisible when things go wrong. `recordMessages` catches all errors internally and never throws. If the OpenBat API is unreachable or returns an error, the SDK logs the error to the console and continues — your chatbot's core functionality is never affected.

To monitor SDK health, check the [API reference](./api.md) for capture endpoint response codes.

---

## SDK Package Location

The SDK source lives in `packages/sdk/` within the OpenBat monorepo:
- `packages/sdk/src/client.ts` — `OpenBat` class
- `packages/sdk/src/wrapper.ts` — `withOpenBat` Vercel AI SDK helper
- `packages/sdk/src/types.ts` — TypeScript interfaces

Build: `cd packages/sdk && npm install && npm run build`
