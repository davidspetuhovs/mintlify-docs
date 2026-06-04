# Getting Started with OpenBat

## What This App Does

OpenBat is a conversational analytics platform — essentially "Google Analytics for AI chatbots." It captures conversations between end-users and AI chatbots, then runs automated analysis to surface business intelligence: sentiment trends, churn risk signals, hallucination detection, feature request patterns, and resolution rates.

Unlike LLM observability tools (Langfuse, LangSmith, Helicone) that focus on token counts and trace debugging for engineers, OpenBat is built for **product teams, customer success, and support**. It answers questions like "Which customers are at risk of churning?" and "What are users actually asking for?" rather than "How many tokens did this call use?"

The platform operates on a multi-tenant organization model. Each organization can have multiple chatbots, each with its own API key, conversation history, analysis configuration, and automated workflows. Data flows in via an SDK integration, gets analyzed by configurable AI pipelines, and surfaces through dashboards, reports, and alerting workflows.

## Navigation Structure

### Public Pages
| Section | URL | Purpose |
|---------|-----|--------|
| Landing Page | `/` | Marketing homepage, product overview |
| Use Cases | `/use-cases/*` | Role-specific value propositions (CS, Engineering, Product, Support) |
| Comparisons | `/compare/*` | Head-to-head vs competitors (Langfuse, LangSmith, Helicone, Braintrust, DIY, Manual) |
| Contact | `/contact` | Demo booking form |
| Security | `/security` | Data protection and compliance details |

### Auth Pages
| Page | URL | Purpose |
|------|-----|--------|
| Sign In | `/auth/login` | Email/password login |
| Sign Up | `/auth/sign-up` | New account registration |
| Forgot Password | `/auth/forgot-password` | Password reset request |

### Platform (Authenticated)
| Section | URL | Purpose |
|---------|-----|--------|
| Chatbot List | `/platform` | Organization-scoped dashboard, all chatbots |
| Members | `/platform/members` | Team member management |
| Org Settings | `/platform/settings` | Organization name, deletion |
| **Chatbot Dashboard** | `/platform/[chatbotId]` | Overview with AI chat, metrics cards |
| Conversations | `/platform/[chatbotId]/conversations` | Filterable conversation list |
| Conversation Detail | `/platform/[chatbotId]/conversations/[id]` | Full transcript + analysis |
| Users | `/platform/[chatbotId]/users` | External user directory with health scores |
| Organizations | `/platform/[chatbotId]/organizations` | External customer org directory |
| Query Types | `/platform/[chatbotId]/query-types` | Semantic question clustering |
| Deep Search | `/platform/[chatbotId]/deep-search` | Semantic conversation search |
| Reports | `/platform/[chatbotId]/reports` | AI-generated dashboard reports |
| Workflows | `/platform/[chatbotId]/workflows` | Automated alert workflows |
| System Prompt | `/platform/[chatbotId]/system-prompt` | Versioned prompt management + experiments |
| Analysis Config | `/platform/[chatbotId]/analysis-config` | Analysis pipeline configuration |
| Settings | `/platform/[chatbotId]/settings` | Chatbot settings, billing, API keys, webhooks |
| Onboarding | `/platform/[chatbotId]/onboarding` | SDK setup wizard |

## Key Workflows

### 1. Sign Up & First Chatbot
Start at `/auth/sign-up` → verify email → sign in at `/auth/login` → land on `/platform` → create first chatbot → complete onboarding wizard at `/platform/[chatbotId]/onboarding` (copy API key, integrate SDK).

### 2. Review Conversations
From `/platform/[chatbotId]/conversations`, filter by sentiment, outcome, or flags → click a conversation → view full transcript with analysis tags at `/platform/[chatbotId]/conversations/[id]` → review General/User/Assistant analysis tabs.

### 3. Ask AI About Your Data
On the chatbot overview (`/platform/[chatbotId]`), type a natural-language question into the AI chat interface (e.g., "Which orgs had the most failed conversations this week?").

### 4. Create a Report
Go to `/platform/[chatbotId]/reports` → pick a template (Customer Pulse, Sentiment Distribution, etc.) or create blank → AI generates an interactive dashboard via chat.

### 5. Set Up Automated Alerts
Visit `/platform/[chatbotId]/workflows` → Templates tab → pick a template (e.g., Slack alert on churn risk) → configure conditions and destinations.

### 6. Configure Analysis Pipeline
At `/platform/[chatbotId]/analysis-config`, configure what gets analyzed: sentiment scoring, AI literacy, custom flags, outcome types, translation settings, and persona discovery.

### 7. Manage System Prompt
At `/platform/[chatbotId]/system-prompt`, edit the prompt in a versioned editor → publish → use experiments tab for A/B testing prompt changes.

### 8. Invite Team Members
From `/platform/members` → open invite modal → set email, org role (Admin/Member), chatbot access, and chatbot role (Editor/Viewer).

### 9. Export Data
Go to `/platform/[chatbotId]/settings` → Import/Export Data tab → download conversations as JSON/CSV with analysis results.

### 10. Explore Demo
From `/platform`, click a Demo-tagged chatbot to browse a read-only dashboard with sample data — no SDK integration needed.