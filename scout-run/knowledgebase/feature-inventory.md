# Feature Inventory

## 1. Authentication & User Management

### Email/Password Authentication
- **Description:** Standard email/password login and registration with email verification
- **URLs:** `/auth/login`, `/auth/sign-up`, `/auth/sign-up-success`, `/auth/confirm`
- **Related Flows:** Email login, Email sign up

### Password Reset
- **Description:** Self-service password reset via email link
- **URLs:** `/auth/forgot-password`, `/auth/update-password`
- **Related Flows:** Password reset request

### Organization & Team Management
- **Description:** Multi-tenant organization model with role-based access (Owner/Admin/Member). Invite members with granular chatbot-level permissions (Editor/Viewer)
- **URLs:** `/platform/members`, `/platform/settings`, `/platform/invitations/accept`
- **Related Flows:** Invite team member

---

## 2. Chatbot Management

### Chatbot CRUD
- **Description:** Create, view, configure, and delete chatbots within an organization. Chatbots have statuses: Active, Pending, Archive, Demo. Card and list view toggles.
- **URL:** `/platform`
- **Related Flows:** Create new chatbot, Explore demo chatbot

### Chatbot Onboarding
- **Description:** Guided SDK setup wizard for newly created chatbots — copy API key, integrate SDK, mark complete
- **URL:** `/platform/[chatbotId]/onboarding`
- **Related Flows:** Create new chatbot

### Chatbot Settings
- **Description:** 7-tab settings panel: General (name, toggles, delete), Billing (Pro $39/mo, credits), Company Info (product context for hallucination detection), API Keys (manage/rotate), Members (chatbot-level access), Webhooks (Discord/Slack/custom), Import/Export
- **URL:** `/platform/[chatbotId]/settings`
- **Related Flows:** Export conversation data

---

## 3. Conversation Analytics

### Conversation List
- **Description:** Filterable, sortable data table of all conversations with outcome, sentiment, flags, and message counts. Supports text search, faceted filters, date range, column customization, and pagination.
- **URL:** `/platform/[chatbotId]/conversations`
- **Related Flows:** Review a specific conversation

### Conversation Detail
- **Description:** Full message transcript with color-coded bubbles (user=pink, assistant=green), translation indicators, analysis tags, expandable reasoning sections. Three analysis tabs: General (flags, outcomes), User (user-specific), Assistant (assistant-specific).
- **URL:** `/platform/[chatbotId]/conversations/[id]`
- **Related Flows:** Review a specific conversation

### Deep Search
- **Description:** Semantic search that finds conversations by meaning rather than keywords
- **URL:** `/platform/[chatbotId]/deep-search`

### Query Types
- **Description:** Automatic semantic clustering of user messages into canonical question categories with volume, intent, sentiment, and resolution rates
- **URL:** `/platform/[chatbotId]/query-types`

---

## 4. User & Organization Intelligence

### External User Directory
- **Description:** Directory of end-users interacting with the chatbot. Shows health scores, personas, AI literacy scores, conversation counts. Filterable and sortable.
- **URL:** `/platform/[chatbotId]/users`

### External Customer Organizations
- **Description:** Directory of customer organizations (populated from SDK metadata). Shows empty state when no org data captured.
- **URL:** `/platform/[chatbotId]/organizations`
- **Note:** Appears to show empty state — may be newly launched or require SDK org metadata to populate.

---

## 5. AI-Powered Features

### Platform AI Chat
- **Description:** Natural-language interface on the chatbot overview for querying analytics data. Supports quick-access commands (tag entity, scope by plan, analysis type).
- **URL:** `/platform/[chatbotId]`
- **Related Flows:** Ask AI about chatbot data

### AI Reports
- **Description:** Chat-driven dashboard builder using AI-generated OpenUI widgets. Pre-built templates: Customer Pulse, Sentiment Distribution, Risk Flags Leaderboard, Topics & Intents Overview. Blank report option available.
- **URL:** `/platform/[chatbotId]/reports`
- **Related Flows:** Create report from template

---

## 6. Analysis Pipeline Configuration

### Analysis Config
- **Description:** 7-tab configuration center controlling the analysis pipeline:
  - **Integration:** 5-layer maturity model from baseline to DB-backed prompt
  - **Metadata:** Managed and SDK-discovered custom fields
  - **Translation:** Auto-translate toggle with primary language selection
  - **User Analysis:** Sentiment scoring, AI literacy, custom flag definitions
  - **Assistant Analysis:** Outcome types, issue types with custom definitions
  - **Calibration:** Training examples for analysis accuracy
  - **Personas:** AI-generated user persona cards with auto-discovery
- **URL:** `/platform/[chatbotId]/analysis-config`
- **Related Flows:** Configure analysis definitions

---

## 7. System Prompt Management

### Versioned Prompt Editor
- **Description:** Full prompt lifecycle management with version timeline, publish mode toggle, kill switch, rollback, and diff view. Three tabs: Prompt (editor), Experiments (A/B testing), Suggested (AI suggestions — coming soon). Shows maturity progression: Manual → Half-automated → Fully automated.
- **URL:** `/platform/[chatbotId]/system-prompt`
- **Related Flows:** Create new prompt version
- **Note:** "Suggested" tab marked as coming soon — placeholder/incomplete feature.

---

## 8. Workflow Automation

### Workflows
- **Description:** Automated alert workflows triggered by analysis conditions. Three tabs: Workflows (list), Runs (execution history with status filtering), Templates (categorized: Alerting, Escalation, Reporting, Moderation, General).
- **URL:** `/platform/[chatbotId]/workflows`
- **Related Flows:** Create workflow from template

---

## 9. Overview Dashboard

### Chatbot Overview
- **Description:** Primary analytics dashboard with summary metric cards: At-Risk Orgs, Performance (Resolution %, Quality Issues, AI Literacy), Activity (conversation count), Risks (churn risks, yes-man, hallucinations). Includes sparkline charts and clickable metrics.
- **URL:** `/platform/[chatbotId]`

---

## 10. Data Import/Export

### Export
- **Description:** JSON/CSV export of conversation data with analysis results
- **URL:** `/platform/[chatbotId]/settings` (Import/Export Data tab)
- **Related Flows:** Export conversation data

### Import
- **Description:** CSV/JSON import capability
- **URL:** `/platform/[chatbotId]/settings` (Import/Export Data tab)

---

## 11. Marketing & Public Pages

### Landing Page
- **Description:** Full marketing homepage with hero, problem/solution narrative, feature walkthroughs, SDK code samples (multi-language tabs), FAQ, CTAs
- **URL:** `/`

### Use Case Pages
- **Description:** Role-targeted marketing pages for Customer Success, Engineering, Product Teams, and Support
- **URLs:** `/use-cases`, `/use-cases/customer-success`, `/use-cases/engineering`, `/use-cases/product-teams`, `/use-cases/support`

### Comparison Pages
- **Description:** Head-to-head competitive comparison pages vs Langfuse, LangSmith, Helicone, Braintrust, Manual Review, and DIY
- **URLs:** `/compare`, `/compare/langfuse`, `/compare/langsmith`, `/compare/helicone`, `/compare/braintrust`, `/compare/manual-review`, `/compare/diy`

### Contact & Security
- **Description:** Demo booking form and security/compliance documentation
- **URLs:** `/contact`, `/security`

---

## Incomplete / Placeholder Features

| Feature | Location | Status |
|---------|----------|--------|
| AI Suggested Prompt Improvements | `/platform/[chatbotId]/system-prompt` → Suggested tab | "Coming soon" |
| External Customer Organizations | `/platform/[chatbotId]/organizations` | Shows empty state — requires SDK org metadata |