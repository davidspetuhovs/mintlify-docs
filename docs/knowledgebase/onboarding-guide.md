# Getting Started with OpenBat

## What This App Does

OpenBat is an AI chatbot analytics platform — essentially "Google Analytics for AI chatbots." It allows teams to monitor, analyze, and optimize their AI-powered chat experiences by ingesting conversation data via SDK or API and running AI-driven analysis on every message.

The platform provides sentiment scoring, topic detection, intent classification, user behavior flagging, and assistant performance analysis across all conversations. It surfaces actionable insights like churn risk signals, frustrated users, capability gaps, and resolution outcomes — enabling teams to understand not just *what* users are asking, but *how well* the chatbot is performing.

OpenBat also includes a workflow automation engine for triggering alerts and actions based on conversation patterns, semantic deep search for finding conversations by meaning, and a client management layer that tracks organizations and individual users with revenue metrics (MRR, plan tier).

## Navigation Structure

### Public Pages
| Page | URL | Purpose |
|------|-----|---------|
| Landing Page | `/` | Marketing site with product demos, pricing, integration examples |
| Login | `/auth/login` | Email/password + social auth (Apple, Google, Meta) |
| Sign Up | `/auth/sign-up` | Account creation |
| Forgot Password | `/auth/forgot-password` | Password reset request |

### Authenticated Platform
| Page | URL | Purpose |
|------|-----|---------|
| Dashboard | `/platform` | Organization-level chatbot list |
| Members | `/platform/members` | Org member management |
| Org Settings | `/platform/settings` | Org rename and deletion |
| Chatbot Dashboard | `/platform/{chatbotId}` | Analytics hub for a specific chatbot |
| Workflows | `/platform/{chatbotId}/workflows` | Automation rules and execution history |
| Conversations | `/platform/{chatbotId}/conversations` | Browsable conversation table |
| Conversation Detail | `/platform/{chatbotId}/conversations/{conversationId}` | Full transcript with analysis annotations |
| Deep Search | `/platform/{chatbotId}/deep-search` | Semantic conversation search |
| Organizations | `/platform/{chatbotId}/organizations` | Client organization metrics |
| Users | `/platform/{chatbotId}/users` | Individual user metrics |
| Analysis Config | `/platform/{chatbotId}/analysis-config` | AI analysis settings and prompts |
| Chatbot Settings | `/platform/{chatbotId}/settings` | API keys, webhooks, import/export |

## Key Workflows

### 1. Create and Configure a Chatbot
Start at `/platform` → Click "Create chatbot" → Name it → Navigate to `/platform/{chatbotId}/settings` to get API keys and configure webhooks.

### 2. Monitor Chatbot Performance
Start at `/platform/{chatbotId}` → Review KPI cards (conversations, messages, sentiment, analyzed today) → Switch between "User Insights" and "Assistant Performance" tabs → Adjust date range and segment filters.

### 3. Investigate Dissatisfied Users
Start at `/platform/{chatbotId}` → Scroll to "Most Dissatisfied Users" → Click "Investigate" → View their conversation threads with annotated sentiment, behavior flags, and resolution status.

### 4. Set Up Workflow Automation
Start at `/platform/{chatbotId}/workflows` → Go to "Templates" tab → Choose a template (alerting, escalation, reporting, moderation) → Or create from scratch in the "Workflows" tab.

### 5. Search Conversations by Meaning
Start at `/platform/{chatbotId}/deep-search` → Enter a natural language query like "users asking about pricing" → Review semantically matched conversations.

### 6. Configure Analysis Settings
Start at `/platform/{chatbotId}/analysis-config` → Enable/disable sentiment scoring, behavior flags, translation → Customize AI prompts for analysis → Track metadata fields discovered from the SDK.

### 7. Manage Team Access
Start at `/platform/members` → Invite members by email with role assignment (Admin/Member) → Manage chatbot-level access at `/platform/{chatbotId}/settings` → Members tab.

### 8. Export and Import Data
Start at `/platform/{chatbotId}/settings` → "Import/Export Data" tab → Export conversations as JSON (with optional analysis) → Import historical data from JSON/CSV.