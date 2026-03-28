# Architecture — OpenBat

## Inferred Tech Stack

### Frontend
- **Framework:** Next.js (App Router) — inferred from URL routing patterns (`/platform/{chatbotId}/...`), the presence of dynamic route segments, and the marketing site / app split architecture.
- **UI Library:** Likely shadcn/ui + Tailwind CSS — suggested by the component patterns (modals, tabs, accordions, data tables, badges, date range pickers, cards) and the level of design consistency.
- **Charts:** Charting library (likely Recharts or similar) for sentiment trends, donut charts, activity heatmaps.
- **State Management:** Primarily URL-driven (route params, search params for filters) with client-side state for modals, tabs, and form inputs.

### Backend
- **API:** Next.js Route Handlers or Server Actions — the app appears to be a full-stack Next.js application given the tight integration between pages and data.
- **AI/ML Pipeline:** Server-side AI analysis using LLM providers (sentiment scoring, intent classification, topic detection, flag identification, semantic search). Multiple configurable prompts suggest a prompt-based pipeline rather than fine-tuned models.
- **Semantic Search:** Vector database or embedding-based search system for the Deep Search feature (semantic similarity rather than keyword matching).

### Authentication
- **Model:** Email/password + social OAuth (Apple, Google, Meta).
- **Session:** Cookie-based or JWT sessions — social auth suggests OAuth integration with redirect flows.
- **Authorization:** Multi-tenant with organization-level and chatbot-level access. Roles observed: Owner, Admin, Member. Two-level member management (org-level and chatbot-level).

### Data Ingestion
- **SDK/API:** Four integration methods (Vercel AI SDK, TypeScript, Python, REST API). Chatbots receive data via API keys (masked, rotatable).
- **Metadata:** SDK can send custom metadata fields that are auto-discovered and require Track/Accept/Deny.
- **Webhooks (Outbound):** Discord, Slack, and custom endpoint support for workflow triggers.

---

## URL Structure & Data Model

```
/                                          → Public marketing
/auth/*                                    → Authentication (login, sign-up, forgot-password)
/platform                                  → Organization-scoped chatbot list
/platform/members                          → Organization.members[]
/platform/settings                         → Organization settings
/platform/{chatbotId}                      → Chatbot dashboard
/platform/{chatbotId}/workflows            → Chatbot.workflows[]
/platform/{chatbotId}/conversations        → Chatbot.conversations[]
/platform/{chatbotId}/conversations/{id}   → Conversation detail
/platform/{chatbotId}/deep-search          → Semantic search across conversations
/platform/{chatbotId}/organizations        → Chatbot.clientOrganizations[]
/platform/{chatbotId}/users                → Chatbot.clientUsers[]
/platform/{chatbotId}/analysis-config      → Chatbot.analysisConfig
/platform/{chatbotId}/settings             → Chatbot settings
```

### Implied Entity Relationships

```
User (platform user)
  └── belongs to → Organization (many-to-many, with roles)
        └── has many → Chatbot
              ├── has many → Conversation
              │     └── has many → Message
              │           └── has many → AnalysisAnnotation (sentiment, flags, quality, resolution)
              ├── has many → Workflow
              │     └── has many → WorkflowRun
              ├── has many → ClientOrganization (end-user orgs)
              │     └── has many → ClientUser
              ├── has one → AnalysisConfig
              │     ├── MetadataFields[]
              │     ├── UserFlags[]
              │     ├── AssistantBehaviors[]
              │     └── AnalysisPrompts[]
              ├── has many → ApiKey
              ├── has many → Webhook
              └── has many → ChatbotMember (chatbot-level access)
```

### Key Observations

- **Multi-tenancy:** Two-level: Platform organizations (who use OpenBat) and client organizations (end-users of the chatbot). These are separate entities — `Organization` at `/platform/members` vs `ClientOrganization` at `/platform/{chatbotId}/organizations`.
- **Revenue tracking:** Client entities have MRR and plan fields — OpenBat tracks customer revenue data for churn/buying signal analysis.
- **Session tracking:** Conversation detail shows session metadata (session ID, page URL, referrer, device, country) — the SDK captures browser context.

---

## Authentication & Authorization Model

| Level | Scope | Roles Observed | URL |
|-------|-------|---------------|-----|
| Organization | All chatbots in org | Owner, Admin, Member | `/platform/members` |
| Chatbot | Single chatbot | Member (addable) | `/platform/{chatbotId}/settings` → Members tab |

- Organization ownership includes a dangerous "delete org" action.
- The sidebar org switcher implies the authenticated user's token/session carries org context.
- Social auth (Apple/Google/Meta) likely maps to the same user accounts as email auth.

---

## State Management Patterns

### URL-Driven State
- **Route params:** `chatbotId`, `conversationId` — primary navigation state.
- **Date range:** Used across dashboard, conversations, deep search, organizations — likely URL search params or a shared context.
- **Tab state:** Multiple pages use tabs (dashboard: User Insights/Assistant Performance, workflows: Workflows/Runs/Templates, analysis config: 5 tabs, settings: 6 tabs) — likely URL hash or search param.
- **Filters:** Conversation table supports search, column sorting, column visibility, pagination — suggests client-side table state with server-side data fetching.

### Client-Side State
- **Modals:** Create chatbot, invite member — transient UI state.
- **Form state:** Analysis config toggles, custom flags, prompt editing.

### Real-Time Indicators
- **"Analyzed Today" KPI** suggests near-real-time analysis pipeline or batch processing with daily counts.
- **Workflow runs** with status (Pending, Triggered, Skipped, Success, Failed) suggest async job processing.
- **Last activity timestamps** on chatbots, conversations, organizations, and users suggest periodic data refresh.

---

## API Surface (Inferred)

### External API (SDK → OpenBat)
- Conversation ingestion endpoint (authenticated via API key)
- Message streaming/batch endpoint
- Metadata field submission
- Session context submission (page URL, referrer, device, country)

### Internal API (Frontend → Backend)
- CRUD: Organizations, Chatbots, Members, Workflows, Webhooks
- Analytics: Dashboard KPIs, sentiment trends, resolution outcomes, activity heatmaps
- Search: Conversation filtering (keyword), Deep Search (semantic/vector)
- Config: Analysis flags, prompts, translation settings, metadata tracking
- Data: Import/export conversations
- Auth: Login, signup, password reset, social OAuth

### Outbound Integrations
- Webhook delivery to Discord, Slack, custom URLs
- Social OAuth (Apple, Google, Meta)
- AI/LLM provider(s) for analysis pipeline

---

## Architectural Patterns

1. **Chatbot-scoped everything:** Once inside a chatbot context, all sub-resources (conversations, workflows, users, orgs, config, settings) are scoped to that chatbot ID. This suggests a strong partition key in the database.

2. **Analysis pipeline:** Messages are analyzed asynchronously — the "Analyzed Today" counter and configurable prompts suggest a job queue that processes new messages through LLM-based analysis (sentiment, intent, topics, flags, resolution). The analysis config page allows customizing this pipeline per chatbot.

3. **Semantic search:** Deep Search requires a vector embedding infrastructure — likely an embedding model + vector database (Pinecone, pgvector, or similar) indexing conversation content.

4. **Workflow engine:** Template-based and custom workflows with execution tracking (runs with statuses). Likely a simple state machine or rule engine evaluating conditions against analyzed conversation data and dispatching actions (webhook calls, alerts).

5. **Multi-SDK support:** Four integration methods (Vercel AI SDK, TypeScript, Python, REST API) suggest a well-defined REST API as the foundation, with typed SDKs wrapping it.