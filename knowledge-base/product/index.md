# OpenBat Knowledge Base

> Turn chatbot conversations into actionable business intelligence — automatically.

OpenBat is a conversational analytics platform for SaaS teams managing AI chatbots. It ingests conversation data through a lightweight SDK, runs LLM-powered analysis on every message, and surfaces insights through dashboards, custom reports, and automated workflows.

---

## Quick Navigation

### Platform Pages
| Section | Route | What It Does |
|---------|-------|-------------|
| [Auth](./pages/auth.md) | `/auth/*` | Login, sign-up, password recovery |
| [Platform Home](./pages/platform-home.md) | `/platform` | Chatbot grid, org management, team members |
| [Dashboard](./pages/dashboard.md) | `/platform/[chatbotId]` | User + assistant analytics, sentiment trends |
| [Conversations](./pages/conversations.md) | `/platform/[chatbotId]/conversations` | Filtered conversation explorer + detail view |
| [Deep Search](./pages/deep-search.md) | `/platform/[chatbotId]/deep-search` | Semantic search across all conversations |
| [Translation](./pages/translation.md) | Settings → Translation tab | Auto-detect and translate 27 languages |
| [Users & Organizations](./pages/users-organizations.md) | `/platform/[chatbotId]/users` | External user and org browsing |
| [Reports](./pages/reports.md) | `/platform/[chatbotId]/reports` | Custom dashboards with configurable widgets |
| [Workflows](./pages/workflows.md) | `/platform/[chatbotId]/workflows` | Automated alerts and actions |
| [Settings](./pages/settings.md) | `/platform/[chatbotId]/settings` | API keys, metadata schema, analysis config |

### Technical Reference
| Doc | Description |
|-----|-------------|
| [Product Overview](./product.md) | What OpenBat is, who it's for, core value props |
| [Analysis Pipeline](./analysis-pipeline.md) | How LLM analysis works end-to-end |
| [SDK](./sdk.md) | Integration guide for capturing conversations |
| [API](./api.md) | REST endpoint reference |

---

## What OpenBat Does in 60 Seconds

1. **You integrate the SDK** — one function call wraps your existing AI chatbot response handler
2. **Conversations flow in** — every message is captured with user, org, and session metadata
3. **LLM analysis runs automatically** — sentiment, intent, topics, flags, behavior, and outcome are extracted from each message
4. **Insights surface in the dashboard** — sentiment trends, frustrated users, capability gaps, response quality scores
5. **Workflows fire alerts** — Slack or webhook notifications trigger when conditions match (e.g., churn risk detected)

---

## Core Features at a Glance

| Feature | Description |
|---------|-------------|
| **Sentiment Analysis** | Per-message sentiment scoring (−1 to +1) with chunk-level reasoning |
| **Intent Classification** | Each user message classified into one intent from your custom list |
| **Topic Detection** | Up to 3 topics extracted per user message, auto-discovered from conversation patterns |
| **Flag Detection** | Business signals flagged per message (churn risk, buying signal, frustrated user, etc.) |
| **Assistant Behavior** | Assistant responses classified by behavior (hallucinating, dodging, helpful, etc.) |
| **Resolution Outcomes** | Conversation outcomes tracked (fully resolved, capability failure, deflected, etc.) |
| **Response Quality** | Multi-dimension scoring (relevance, completeness, clarity, accuracy, tone) |
| **Deep Search** | Semantic search across all messages — find by meaning, not just keywords |
| **Auto-Translation** | 27 languages detected and translated automatically; analysis runs on translated text |
| **Conversation Explorer** | Full-text search + faceted filtering across all conversations |
| **Custom Reports** | Configurable dashboards with 14 widget types |
| **Workflow Automation** | Visual workflow builder with trigger → condition → webhook action chain |
| **Team Access** | Role-based org and chatbot access (owner, admin, member) |
| **Multi-chatbot** | One org supports unlimited chatbots, each with its own API key and settings |

---

## Data Model Summary

```
organizations
  └── chatbots (each has a unique API key)
        └── conversations (one per external conversation ID)
              └── messages (role: user / assistant / system)
                    ├── user_sentiments        (score, chunk, reasoning)
                    ├── user_intents           (value, confidence, reasoning)
                    ├── user_topics            (0–3 per message)
                    ├── user_flags             (0+ per message)
                    ├── assistant_behaviors    (1 per assistant message)
                    ├── assistant_outcomes     (1 per assistant message)
                    ├── assistant_qualities    (dimensions array)
                    └── assistant_flags        (0+ per message)

workflows               (triggers + conditions + webhook actions)
analysis_definitions    (per-chatbot intent/topic/flag vocabulary)
llm_calls               (audit log of every Gemini call)
```

---

## Tech Stack

- **Framework:** Next.js 16 (App Router, Turbopack)
- **Database:** Supabase (PostgreSQL 17, Auth, RLS)
- **LLM:** Google Gemini via `@google/genai` (direct SDK, not AI SDK)
- **Workflow Engine:** Vercel Workflow DevKit (durable, retryable steps)
- **UI:** shadcn/ui v4 (radix-nova), Tailwind CSS v4, Recharts
- **Design:** Dark mode only, purple/indigo accent `oklch(0.65 0.19 270)`
