# Architecture Overview

## Tech Stack

### Frontend
- **Framework:** Next.js (App Router) — inferred from URL structure (`/platform/[chatbotId]/...` dynamic segments), server-side rendering patterns, and overall SPA behavior
- **UI Library:** Tailwind CSS with a component library (likely shadcn/ui based on consistent dark-themed form elements, cards, tables, tabs, modals, and dialog patterns)
- **Charting:** Sparkline charts in overview dashboard, data tables with sorting/filtering/pagination suggest Recharts or similar
- **Workflow Editor:** Visual workflow builder on the workflows page suggests a node-based editor (possibly XYFlow/ReactFlow)
- **Theme:** Dark mode only — consistent across all pages with no light mode toggle observed

### Backend
- **API Structure:** RESTful API at `/api/v1/*` based on standard patterns
- **Authentication:** Session-based auth with email/password (cookie-based sessions inferred from redirect behavior). Organization-scoped access control with roles: Owner, Admin, Member at org level; Editor, Viewer at chatbot level
- **AI/LLM:** Platform AI chat and AI-generated reports indicate server-side LLM integration with streaming responses
- **Workflows:** Durable workflow execution with status tracking (Pending, Triggered, Skipped, Success, Failed) — suggests a workflow engine with persistent state

### Database
- **Type:** PostgreSQL (inferred from relational data model complexity, faceted filtering, pagination)
- **Key Entities:** Organizations, Members, Chatbots, Conversations, Messages, Analyses, Workflows, Reports, Prompt Versions, API Keys

## Authentication Model

### Two Auth Contexts
1. **Dashboard Auth (Session-based):** Email/password login at `/auth/login` → session cookie → all `/platform/*` routes protected. Unauthenticated requests redirect to `/auth/login`. Supports email verification, password reset.
2. **SDK/API Auth (API Key):** Chatbot-specific API keys (format: `ob_live_*`) for SDK data ingestion at `/api/v1/capture`. Keys are rotatable from settings.

### Role-Based Access Control
- **Organization level:** Owner (full control including deletion), Admin (member management), Member (read/use)
- **Chatbot level:** Editor (modify settings, configs), Viewer (read-only)
- **Invitation flow:** Email invite with role assignment → accept at `/platform/invitations/accept`

### Auth Edge Cases Observed
- Pending role users are redirected to `/auth/pending`
- Banned users redirected to `/auth/login?error=banned`
- Email verification required before first login

## URL Patterns & Data Model

### URL Hierarchy
```
/platform                                    → Organization scope (implicit from session)
/platform/[chatbotId]                        → Chatbot scope
/platform/[chatbotId]/conversations          → Conversation list
/platform/[chatbotId]/conversations/[id]     → Single conversation
```

This suggests a data hierarchy:
```
Organization (1)
  └── Chatbot (many)
        └── Conversation (many)
              └── Message (many)
                    └── Analysis (many, per message)
```

### Additional Entities (inferred from URLs)
- **Users** (`/platform/[chatbotId]/users`): External end-users tracked per chatbot
- **Organizations** (`/platform/[chatbotId]/organizations`): External customer orgs (SDK metadata)
- **Reports** (`/platform/[chatbotId]/reports`): AI-generated dashboards per chatbot
- **Workflows** (`/platform/[chatbotId]/workflows`): Automation rules per chatbot
- **Query Types** (`/platform/[chatbotId]/query-types`): Clustered question categories per chatbot
- **System Prompt** (`/platform/[chatbotId]/system-prompt`): Versioned prompts per chatbot

### API Patterns
- `/api/v1/capture` — SDK ingestion endpoint (API key auth)
- `/api/v1/chatbots/*` — Chatbot CRUD (session auth)
- `/api/v1/conversations/*` — Conversation endpoints (session auth)
- `/api/v1/analytics/*` — Analytics aggregation (session auth)
- `/api/v1/export/[chatbotId]` — Data export (session auth)
- `/api/auth/[...all]` — Auth catch-all handler
- `/api/chat` — Platform AI chat (streaming)
- `/api/ai-reports/[reportId]/*` — AI report chat and tool execution

## State Management Patterns

### URL-Based State
- **Tabs:** Tab state appears managed via UI component state (not URL params) — tabs for chatbot status filters (Active/Pending/Archive/Demo), analysis config sections, settings sections
- **Pagination:** Table pagination with page numbers (604 rows, 31 pages observed in conversations)
- **Filters:** Faceted filters, text search, date range pickers on data tables
- **Dynamic Segments:** `[chatbotId]` and conversation `[id]` in URL path

### Real-Time / Streaming Indicators
- **AI Chat:** Streaming responses in platform AI chat and AI reports
- **Workflow Runs:** Status tracking (Pending → Triggered → Success/Failed) suggests polling or real-time updates
- **Sparkline Charts:** Real-time or near-real-time metric visualization on overview dashboard

### Analysis Pipeline Architecture
The analysis pipeline is the core differentiator:
1. **Ingestion:** SDK sends messages via `POST /api/v1/capture` with API key
2. **Storage:** Messages stored in database
3. **Analysis Dispatch:** Workflow engine triggers analysis steps per user-defined definitions
4. **LLM Processing:** Configurable analysis types (sentiment, intent, flags, outcomes, AI literacy, personas)
5. **Results Storage:** Analysis results stored per-message, multiple types per message
6. **Surfacing:** Results appear in conversation detail, aggregate in dashboards, power search and filtering

### Multi-Language SDK Support
Landing page shows SDK code samples in tabs: Vercel AI SDK, TypeScript, Python, REST API — indicating a polyglot SDK strategy.

## Key Architectural Observations

1. **Organization-scoped multi-tenancy:** All data is scoped to an organization. Users can belong to multiple orgs (implied by org switcher patterns).
2. **Chatbot as primary data silo:** Each chatbot is an independent analytics unit with its own conversations, analysis config, workflows, reports, and settings.
3. **Configurable analysis pipeline:** Unlike hardcoded analytics, users define what gets analyzed (custom flags, custom outcome types, calibration examples). This suggests a plugin-like analysis architecture.
4. **AI-native reporting:** Reports are generated conversationally via AI rather than through a traditional dashboard builder — a distinctive architectural choice using OpenUI for widget rendering.
5. **Prompt lifecycle management:** System prompt versioning with timeline, rollback, diff, A/B experiments, and maturity levels indicates sophisticated prompt operations tooling.
6. **Durable workflows:** Workflow execution with status tracking and run history suggests a persistent workflow engine (not simple cron jobs).
7. **Semantic search:** Deep search by meaning (not keywords) implies vector embeddings or similar semantic search infrastructure.