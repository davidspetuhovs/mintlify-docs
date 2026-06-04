# Application Sitemap: http://openbat.dev/auth/login

Generated: 2026-06-04T08:23:49.143Z
Pages discovered: 34
Flows identified: 14

---

## Pages

| # | Page | URL | Description |
|---|---|---|---|
| 1 | [Landing Page](pages/landing-page.md) | `/` | Marketing homepage for OpenBat — positions the product as 'Google Analytics for AI chatbots.' Features hero section, problem/solution narrat |
| 2 | [Sign In](pages/sign-in.md) | `/auth/login` | Email/password authentication page for returning users. Minimal dark-themed form with OpenBat branding, email field, password field, forgot  |
| 3 | [Create Account](pages/create-account.md) | `/auth/sign-up` | Registration page for new users. Collects work email, password, and password confirmation. Sends a verification email on submit. Includes te |
| 4 | [Forgot Password](pages/forgot-password.md) | `/auth/forgot-password` | Password reset request page. User enters their email to receive a one-time reset link. Links back to sign-in. |
| 5 | [Chatbot List (Dashboard)](pages/chatbot-list-dashboard.md) | `/platform` | Organization-scoped dashboard showing all chatbots. Displays chatbot cards with name, plan badge (Pro/Demo), API key prefix, creator email,  |
| 6 | [Organization Members](pages/organization-members.md) | `/platform/members` | Team member management page showing a table of all organization members with email, role (Owner/Admin/Member), and join date. Supports invit |
| 7 | [Organization Settings](pages/organization-settings.md) | `/platform/settings` | Organization-level settings with editable organization name and a danger zone for permanent organization deletion. |
| 8 | [Chatbot Overview Dashboard](pages/chatbot-overview-dashboard.md) | `/platform/[chatbotId]` | Primary chatbot analytics dashboard with an AI chat interface ('What can I help you discover?'), quick-access command hints (tag entity, sco |
| 9 | [Reports](pages/reports.md) | `/platform/[chatbotId]/reports` | AI-native reports page where users can create chat-driven dashboards. Offers pre-built templates (Customer Pulse, Sentiment Distribution, Ri |
| 10 | [Workflows](pages/workflows.md) | `/platform/[chatbotId]/workflows` | Automation hub for creating alert workflows triggered by analysis conditions. Three tabs: Workflows (list), Runs (execution history with sta |
| 11 | [System Prompt](pages/system-prompt.md) | `/platform/[chatbotId]/system-prompt` | Comprehensive system prompt management page with three tabs: Prompt (versioned prompt editor with timeline, publish mode toggle, kill switch |
| 12 | [Users](pages/users.md) | `/platform/[chatbotId]/users` | External chatbot user directory with a sortable, filterable data table. Columns: User (ID), Organization, Health score, Persona, AI Literacy |
| 13 | [Conversations](pages/conversations.md) | `/platform/[chatbotId]/conversations` | Conversation list page with a sortable, filterable data table. Columns: User, Messages count, Outcome (Resolved/Partially Resolved/Failed),  |
| 14 | [Conversation Detail](pages/conversation-detail.md) | `/platform/[chatbotId]/conversations/[id]` | Full conversation transcript view with chat bubbles for user (pink) and assistant (green) messages. Shows translation indicators, analysis t |
| 15 | [Query Types](pages/query-types.md) | `/platform/[chatbotId]/query-types` | Semantic query type clustering page that automatically groups user messages into canonical question categories. Table columns: Query type (n |
| 16 | [Deep Search](pages/deep-search.md) | `/platform/[chatbotId]/deep-search` | Semantic search interface that finds conversations by meaning rather than keywords. Single search input with a 'Deep Search' button and date |
| 17 | [External Customer Organizations](pages/external-customer-organizations.md) | `/platform/[chatbotId]/organizations` | Directory of external customer organizations whose users interact with the chatbot. Populated automatically when the SDK sends organization  |
| 18 | [Analysis Config](pages/analysis-config.md) | `/platform/[chatbotId]/analysis-config` | Comprehensive analysis configuration page with 7 tabs: Integration (5-layer integration maturity from baseline to DB-backed prompt with code |
| 19 | [Chatbot Settings](pages/chatbot-settings.md) | `/platform/[chatbotId]/settings` | Chatbot-level settings with 7 tabs: General (name, ID, creation date, analysis toggles, re-analyze, delete), Billing (Pro plan at $39/mo wit |
| 20 | [Chatbot Onboarding](pages/chatbot-onboarding.md) | `/platform/[chatbotId]/onboarding` | SDK setup wizard for newly created chatbots. Guides users through copying the API key and integrating the OpenBat SDK. Redirects to the dash |
| 21 | [Use Cases Overview](pages/use-cases-overview.md) | `/use-cases` | Marketing page showcasing how different teams use OpenBat. Links to dedicated pages for Customer Success, Engineering, Product Teams, and Su |
| 22 | [Use Case — Customer Success](pages/use-case-customer-success.md) | `/use-cases/customer-success` | Marketing page focused on how CS teams use OpenBat to detect churn risk, surface at-risk accounts, and monitor sentiment before renewal revi |
| 23 | [Use Case — Engineering](pages/use-case-engineering.md) | `/use-cases/engineering` | Marketing page focused on how engineering teams use OpenBat to catch hallucinations, monitor chatbot quality, and validate prompt changes. |
| 24 | [Use Case — Product Teams](pages/use-case-product-teams.md) | `/use-cases/product-teams` | Marketing page focused on how product teams use OpenBat to understand what users ask for, ranked by demand and sentiment. |
| 25 | [Use Case — Support](pages/use-case-support.md) | `/use-cases/support` | Marketing page focused on how support teams use OpenBat to triage frustration and resolve issues faster. |
| 26 | [Compare Overview](pages/compare-overview.md) | `/compare` | Marketing page positioning OpenBat against LLM observability tools. Highlights that competitors count tokens while OpenBat surfaces business |
| 27 | [Compare — vs Langfuse](pages/compare-vs-langfuse.md) | `/compare/langfuse` | Head-to-head comparison page positioning OpenBat (business intelligence for product/CS teams) against Langfuse (LLM tracing for engineers). |
| 28 | [Compare — vs LangSmith](pages/compare-vs-langsmith.md) | `/compare/langsmith` | Comparison page: OpenBat vs LangSmith (tracing tool vs business intelligence). |
| 29 | [Compare — vs Helicone](pages/compare-vs-helicone.md) | `/compare/helicone` | Comparison page: OpenBat vs Helicone (API logs vs conversation insight). |
| 30 | [Compare — vs Braintrust](pages/compare-vs-braintrust.md) | `/compare/braintrust` | Comparison page: OpenBat vs Braintrust (eval suite vs ongoing monitoring). |
| 31 | [Compare — vs Manual Review](pages/compare-vs-manual-review.md) | `/compare/manual-review` | Comparison page: OpenBat vs manual spreadsheet-based conversation review. |
| 32 | [Compare — vs DIY](pages/compare-vs-diy.md) | `/compare/diy` | Comparison page: OpenBat vs building your own analytics pipeline. |
| 33 | [Contact](pages/contact.md) | `/contact` | Demo booking and contact page. Features a live thread illustration showing conversation analysis in action (churn risk detection). Includes  |
| 34 | [Security](pages/security.md) | `/security` | Security information page detailing OpenBat's data protection practices. Covers encryption (TLS 1.2+, AES-256-GCM), data handling, access co |

## All Discovered Flows

- [Sign up from landing page](flows/sign-up-from-landing-page.md)
- [Email login](flows/email-login.md)
- [Email sign up](flows/email-sign-up.md)
- [Password reset request](flows/password-reset-request.md)
- [Create new chatbot](flows/create-new-chatbot.md)
- [Explore demo chatbot](flows/explore-demo-chatbot.md)
- [Invite team member](flows/invite-team-member.md)
- [Ask AI about chatbot data](flows/ask-ai-about-chatbot-data.md)
- [Create report from template](flows/create-report-from-template.md)
- [Create workflow from template](flows/create-workflow-from-template.md)
- [Create new prompt version](flows/create-new-prompt-version.md)
- [Review a specific conversation](flows/review-a-specific-conversation.md)
- [Configure analysis definitions](flows/configure-analysis-definitions.md)
- [Export conversation data](flows/export-conversation-data.md)
