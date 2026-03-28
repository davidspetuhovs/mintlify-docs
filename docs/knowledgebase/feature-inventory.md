# Feature Inventory — OpenBat

## 1. Authentication & Account Management

### Email/Password Authentication
- **Description:** Standard email and password login and registration with password confirmation.
- **URLs:** `/auth/login`, `/auth/sign-up`
- **Related Flows:** Email login, Email sign up

### Social Authentication
- **Description:** Sign in/up via Apple, Google, and Meta OAuth providers.
- **URLs:** `/auth/login`, `/auth/sign-up`
- **Related Flows:** Social auth login

### Password Reset
- **Description:** Self-service password reset via email.
- **URL:** `/auth/forgot-password`
- **Related Flows:** Forgot password flow, Password reset

---

## 2. Organization Management

### Multi-Organization Support
- **Description:** Users can belong to multiple organizations and switch between them via a sidebar switcher. Each organization has its own set of chatbots, members, and settings.
- **URL:** `/platform` (sidebar switcher)
- **Related Flows:** Switch organization

### Member Management
- **Description:** Invite and manage organization members with role-based access (Owner, Admin, Member).
- **URL:** `/platform/members`
- **Related Flows:** Invite a team member

### Organization Settings
- **Description:** Rename organization and permanently delete organization (danger zone).
- **URL:** `/platform/settings`
- **Related Flows:** Rename organization, Delete organization

---

## 3. Chatbot Management

### Chatbot Dashboard
- **Description:** Card/list view of all chatbots in the current org, showing key metrics (API key prefix, creator, last activity, conversation/message counts). Filterable by status: Active, Pending, Archive.
- **URL:** `/platform`
- **Related Flows:** Open a chatbot, Create a new chatbot

### Chatbot Creation
- **Description:** Modal-based chatbot creation with name field (100 char limit) and setup wizard.
- **URL:** `/platform` (modal)
- **Related Flows:** Create a new chatbot

### Chatbot Settings
- **Description:** Six-tab configuration: General (name, ID, creation date), Company Info (onboarding wizard — **appears incomplete/placeholder**), API Keys (view, copy, rotate), Members (chatbot-level access), Webhooks (Discord, Slack, custom), Import/Export Data.
- **URL:** `/platform/{chatbotId}/settings`
- **Related Flows:** Configure API keys, Configure webhooks, Export/Import conversation data
- **Note:** "Company Info" tab shows empty state requiring onboarding wizard — may be incomplete.

---

## 4. Conversation Analytics

### KPI Dashboard
- **Description:** Top-level metrics cards: Conversations count, Messages count, Average Sentiment, Analyzed Today. Date range selector and segment filter (by Plan).
- **URL:** `/platform/{chatbotId}`
- **Related Flows:** Change analysis time period

### User Insights
- **Description:** Comprehensive user-focused analytics tab including: sentiment trends chart, top frustrations, most dissatisfied users (with investigate links), support topics, revenue signals (churn risk, buying signals, capability gaps), top intents, sentiment by segment, activity heatmap, and languages breakdown.
- **URL:** `/platform/{chatbotId}` (User Insights tab)
- **Related Flows:** Investigate a dissatisfied user

### Assistant Performance
- **Description:** AI assistant quality analysis: behavior alerts, resolution outcomes (donut chart), quality flags table, capability gaps.
- **URL:** `/platform/{chatbotId}` (Assistant Performance tab)

### Conversation Browser
- **Description:** Fully featured data table of all conversations with columns for User, Email, Organization, Messages, Sentiment (color-coded), Plan, Last Message, Created. Supports search, filtering, column sorting, date range, column visibility toggling, and pagination.
- **URL:** `/platform/{chatbotId}/conversations`
- **Related Flows:** Filter conversations, View conversation detail

### Conversation Detail
- **Description:** Full message thread with clickable AI analysis annotations — sentiment tags, behavior flags, quality flags, and resolution status per message. Right sidebar with metadata: overall sentiment score/distribution, conversation info, user info (name, email, user ID, plan, industry, MRR), organization info, and session info (session ID, page URL, referrer, device, country).
- **URL:** `/platform/{chatbotId}/conversations/{conversationId}`
- **Related Flows:** View conversation detail, Review message-level analysis

---

## 5. Semantic Search

### Deep Search
- **Description:** Meaning-based search across all conversations using semantic similarity rather than keyword matching. Supports natural language queries like "users asking about pricing" or "billing issues." Includes date range filtering.
- **URL:** `/platform/{chatbotId}/deep-search`
- **Related Flows:** Semantic search conversations

---

## 6. Client Management

### Organizations (Clients)
- **Description:** Table of all customer organizations that interacted with the chatbot. Metrics: name, plan tier, industry, MRR, conversation count, user count, average sentiment, last activity. Supports search, filtering, sorting, date range, column visibility.
- **URL:** `/platform/{chatbotId}/organizations`
- **Related Flows:** Browse client organizations

### Users (Clients)
- **Description:** Table of individual end-users: name, email, organization, plan, MRR, conversation count, sentiment, last activity. Supports search, sorting, pagination.
- **URL:** `/platform/{chatbotId}/users`
- **Related Flows:** Browse chatbot users

---

## 7. Workflow Automation

### Workflow Builder
- **Description:** Create automated workflows triggered by conversation patterns. Supports custom creation with name, conditions, and actions. Empty state when no workflows exist.
- **URL:** `/platform/{chatbotId}/workflows` (Workflows tab)
- **Related Flows:** Create a workflow from scratch

### Workflow Templates
- **Description:** Six pre-built templates categorized as Alerting, Escalation, Reporting, Moderation, and General.
- **URL:** `/platform/{chatbotId}/workflows` (Templates tab)
- **Related Flows:** Create a workflow from template

### Workflow Runs
- **Description:** Execution history with status filtering: All, Pending, Triggered, Skipped, Success, Failed.
- **URL:** `/platform/{chatbotId}/workflows` (Runs tab)

---

## 8. Analysis Configuration

### Metadata Management
- **Description:** Discover and manage custom metadata fields sent via SDK. Track/Accept/Deny controls per field.
- **URL:** `/platform/{chatbotId}/analysis-config` (Metadata tab)
- **Related Flows:** Track metadata fields

### Auto-Translation
- **Description:** Toggle automatic translation of non-primary-language messages with primary language selector.
- **URL:** `/platform/{chatbotId}/analysis-config` (Translation tab)
- **Related Flows:** Enable auto-translation

### User Analysis Flags
- **Description:** Enable/disable sentiment scoring and configurable user behavior flags: Churn Risk, Frustrated User, Buying Signal, Competitor Mention, Urgent Request, Confused User. Supports custom flag creation.
- **URL:** `/platform/{chatbotId}/analysis-config` (User Analysis tab)
- **Related Flows:** Configure user analysis flags

### Assistant Behavior Analysis
- **Description:** Classification toggles for assistant behaviors: Helpful, Yes-Man, Dodging, Over-Apologizing, Hallucinating, Redirecting, Verbose, Robotic, Other.
- **URL:** `/platform/{chatbotId}/analysis-config` (Assistant Analysis tab)

### Custom Analysis Prompts
- **Description:** Editable AI prompts for Sentiment, Intent, Topics, and Flags analysis with "Default" labels on unmodified prompts.
- **URL:** `/platform/{chatbotId}/analysis-config` (Prompts tab)
- **Related Flows:** Edit analysis prompts

---

## 9. Integration & Data

### API Keys
- **Description:** View masked API key, copy to clipboard, rotate key with security warning.
- **URL:** `/platform/{chatbotId}/settings` (API Keys tab)
- **Related Flows:** Configure API keys

### Webhooks
- **Description:** Configure webhook destinations for workflow alerts — Discord, Slack, and custom endpoints.
- **URL:** `/platform/{chatbotId}/settings` (Webhooks tab)
- **Related Flows:** Configure webhooks

### Data Import/Export
- **Description:** Export conversations as JSON with optional analysis results. Import from JSON/CSV with downloadable template.
- **URL:** `/platform/{chatbotId}/settings` (Import/Export Data tab)
- **Related Flows:** Export conversation data, Import conversation data

### SDK Integration
- **Description:** Code examples for Vercel AI SDK, TypeScript, Python, and REST API shown on landing page.
- **URL:** `/` (integration code tabs)

---

## 10. Marketing & Onboarding

### Landing Page
- **Description:** Full marketing page with hero section, animated chat widget demo, AI provider logos carousel, feature sections, code integration examples, pricing tiers (Free through Enterprise), FAQ accordion, testimonials, and CTA footer.
- **URL:** `/`
- **Related Flows:** Navigate to sign up, Explore feature demos

---

## Potentially Incomplete Features

| Feature | Location | Observation |
|---------|----------|-------------|
| Company Info | `/platform/{chatbotId}/settings` → Company Info tab | Shows empty state requiring onboarding wizard; forms present but may not be fully wired |
| Workflow Builder | `/platform/{chatbotId}/workflows` | Template flow described but custom builder specifics (conditions/actions UI) unclear |
| Deep Search Results | `/platform/{chatbotId}/deep-search` | Search UI exists but result format and click-through behavior not detailed |