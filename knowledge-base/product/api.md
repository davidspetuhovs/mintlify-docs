# API Reference

OpenBat exposes two categories of endpoints:

1. **SDK Ingestion API** — authenticated with an API key (`ob_live_...`), used by your chatbot integration
2. **Dashboard API** — authenticated with a Supabase session cookie, used by the web dashboard (and available for programmatic access)

Base URL: `https://app.openbat.dev`

---

## Authentication

### SDK Endpoints (API Key)
Pass your chatbot's API key as a Bearer token:
```
Authorization: Bearer ob_live_<32 hex chars>
```

The key is validated by hashing it (SHA-256) and looking up the corresponding chatbot. The full key is never stored — only the hash.

### Dashboard Endpoints (Session)
Uses Supabase cookie-based authentication. Session is established via the web login flow. All dashboard endpoints enforce organization-level RLS — you can only access data that belongs to your organization.

---

## SDK Ingestion

### POST /api/v1/capture

Ingest conversation messages from your chatbot. The primary endpoint your SDK integration calls.

**Auth:** API key (Bearer token)

**Request body:**
```typescript
{
  // Required
  conversationId: string,           // Your unique ID for this conversation

  // Messages (required, 1–100 per call)
  messages: Array<{
    role: "user" | "assistant" | "system",
    content: string,
    id?: string,     // External message ID — used for deduplication
    sentAt?: string  // ISO 8601 datetime
  }>,

  // User metadata (optional)
  user?: {
    id?: string,
    name?: string,
    email?: string,
    plan?: string,
    createdAt?: string,  // ISO 8601
    industry?: string,
    mrr?: number
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

  // Custom fields (optional — validated against chatbot schema)
  custom?: Record<string, string | number | boolean>,

  // Deprecated aliases (still accepted, prefer user/custom above)
  userId?: string,      // Use user.id instead
  metadata?: object     // Use custom instead
}
```

**Response `200 OK`:**
```json
{
  "ok": true,
  "conversationId": "uuid",
  "messagesStored": 2,
  "analysisQueued": true,
  "warnings": ["Custom field 'unknown_field' not in schema"]
}
```

**Response fields:**
| Field | Description |
|-------|-------------|
| `ok` | Always `true` on success |
| `conversationId` | OpenBat's internal UUID for the conversation |
| `messagesStored` | Number of new messages inserted (duplicates excluded) |
| `analysisQueued` | Whether LLM analysis was triggered |
| `warnings` | Non-fatal validation issues (e.g., unknown custom fields) |

**Behavior:**
- Upserts the conversation (creates if new, updates metadata if exists)
- Deduplicates messages by `id` field — same message sent twice is stored once
- Returns immediately — analysis runs asynchronously
- Unknown `custom` fields produce a warning but don't fail the request
- Custom fields that violate the chatbot's schema (wrong type) produce a warning

**Error responses:**
| Status | Meaning |
|--------|---------|
| `401 Unauthorized` | Missing or invalid API key |
| `400 Bad Request` | Invalid request body (missing required fields, wrong types) |
| `429 Too Many Requests` | Rate limit exceeded |

---

## Chatbot Management

### GET /api/v1/chatbots

List all chatbots in the authenticated user's organization.

**Auth:** Session

**Response `200 OK`:**
```json
[
  {
    "id": "uuid",
    "name": "Support Bot",
    "api_key_prefix": "ob_live_a1b2c3...",
    "settings": { "onboarded": true },
    "created_at": "2024-01-15T10:00:00Z"
  }
]
```

---

### POST /api/v1/chatbots

Create a new chatbot. Returns the full API key — shown **only once**.

**Auth:** Session

**Request body:**
```json
{ "name": "My Chatbot" }
```

**Response `200 OK`:**
```json
{
  "ok": true,
  "chatbot": {
    "id": "uuid",
    "name": "My Chatbot",
    "api_key_prefix": "ob_live_a1b2c3...",
    "settings": {},
    "created_at": "2024-01-15T10:00:00Z"
  },
  "apiKey": "ob_live_a1b2c3d4e5f6..."  // Full key — save this now, never shown again
}
```

---

### GET /api/v1/chatbots/:id

Get a single chatbot by ID.

**Auth:** Session

**Response `200 OK`:** Single chatbot object (same shape as list item).

---

### PATCH /api/v1/chatbots/:id

Update a chatbot's name or settings.

**Auth:** Session

**Request body:**
```json
{
  "name": "New Name",
  "settings": { "userAnalysisEnabled": false }
}
```

Both fields are optional. Settings are deep-merged with existing values.

**Response `200 OK`:** Updated chatbot object.

---

### DELETE /api/v1/chatbots/:id

Permanently delete a chatbot and all its data (conversations, messages, analysis results).

**Auth:** Session

**Response `200 OK`:**
```json
{ "ok": true }
```

---

### POST /api/v1/chatbots/:id/rotate-key

Generate a new API key for the chatbot. The old key is immediately invalidated.

**Auth:** Session

**Response `200 OK`:**
```json
{
  "ok": true,
  "chatbot": { ... },
  "apiKey": "ob_live_newkeyhere..."  // New full key — save this now
}
```

---

## Conversations

### GET /api/v1/conversations

List conversations for the authenticated user's chatbots.

**Auth:** Session

**Query parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `chatbotId` | string | — | Filter to a specific chatbot |
| `page` | number | 1 | Page number |
| `limit` | number | 20 | Items per page (max 100) |

**Response `200 OK`:**
```json
{
  "conversations": [
    {
      "id": "uuid",
      "chatbot_id": "uuid",
      "external_conversation_id": "conv_123",
      "external_user_id": "user_456",
      "message_count": 8,
      "first_message_at": "2024-01-15T10:00:00Z",
      "last_message_at": "2024-01-15T10:15:00Z",
      "created_at": "2024-01-15T10:00:00Z",
      "chatbots": { "name": "Support Bot" }
    }
  ],
  "total": 142,
  "page": 1,
  "limit": 20
}
```

---

### GET /api/v1/conversations/:id

Get a single conversation with full message history and analysis.

**Auth:** Session

**Response `200 OK`:**
```json
{
  "id": "uuid",
  "external_conversation_id": "conv_123",
  "message_count": 4,
  "first_message_at": "...",
  "last_message_at": "...",
  "messages": [
    {
      "id": "uuid",
      "role": "user",
      "content": "How do I cancel my subscription?",
      "external_message_id": "msg_001",
      "created_at": "...",
      "user_sentiments": [
        {
          "score": -0.4,
          "text_chunk": "cancel my subscription",
          "reasoning": "User expressing intent to discontinue service"
        }
      ]
    },
    {
      "id": "uuid",
      "role": "assistant",
      "content": "You can cancel by going to Settings...",
      "created_at": "..."
    }
  ]
}
```

---

## Analytics

### GET /api/v1/analytics/overview

Aggregate metrics across all chatbots (or a specific chatbot).

**Auth:** Session

**Query parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `chatbotId` | string | Optional — scope to one chatbot |

**Response `200 OK`:**
```json
{
  "totalConversations": 1247,
  "totalMessages": 8932,
  "avgSentiment": 0.23,
  "sentimentDistribution": {
    "Very Positive": 312,
    "Positive": 445,
    "Neutral": 298,
    "Negative": 142,
    "Very Negative": 50
  },
  "messagesToday": 83
}
```

---

### GET /api/v1/analytics/sentiment

Sentiment trend data for charting, optionally scoped to one chatbot.

**Auth:** Session

**Query parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `chatbotId` | string | — | Required — filter to one chatbot |
| `days` | number | 30 | Lookback period (1–365) |

**Response `200 OK`:**
```json
{
  "sentimentOverTime": [
    { "date": "2024-01-15", "avgScore": 0.18, "count": 42 },
    { "date": "2024-01-16", "avgScore": 0.24, "count": 38 }
  ],
  "distribution": {
    "Positive": 145,
    "Neutral": 89,
    "Negative": 43
  },
  "total": 277
}
```

---

## Demo Chat Endpoint

### POST /api/chat

A demo chat endpoint that streams responses from Gemini and automatically captures the conversation to OpenBat. Used by the demo chat interface.

**Auth:** None (public demo endpoint)

**Request body:**
```json
{
  "messages": [...],
  "metadata": {
    "conversationId": "...",
    "user": { "id": "...", "name": "..." }
  }
}
```

**Response:** Server-sent event stream (Vercel AI SDK UIMessage stream format).

**Side effect:** On completion, `withOpenBat` captures the full conversation including the new assistant response.

---

## Rate Limits & Limits

| Endpoint | Limit |
|----------|-------|
| `/api/v1/capture` | Messages per request: 1–100 |
| `/api/v1/conversations` | Max page size: 100 |
| `/api/v1/analytics/sentiment` | Max `days`: 365 |

---

## API Key Format

```
ob_live_<32 lowercase hex characters>

Example: ob_live_a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4
```

The prefix `ob_live_a1b2c3` (first ~14 chars) is stored in the dashboard for identification. The full key is hashed with SHA-256 — only the hash is stored in the database. The full key is returned **once** at creation or rotation and cannot be recovered.
