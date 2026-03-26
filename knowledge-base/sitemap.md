# Application Sitemap: http://localhost:3000

Generated: 2026-03-26T16:31:25.553Z
Pages discovered: 17
Flows identified: 32

---

## Pages

### 1. Landing Page (`/`)

Public marketing landing page for OpenBat — 'Google Analytics for AI chatbots'. Features hero section with value proposition, animated chat widget demo, logo carousel of supported AI providers, feature sections (conversation analysis, sentiment scoring, topic detection, workflow automation, SDK integration), pricing tiers (Free through Enterprise), FAQ accordion, testimonials, and CTA sections.

**Interactive elements:**
- link: Features (anchor)
- link: Pricing (anchor)
- link: FAQs (anchor)
- link: Login
- link: Sign Up
- link: Start Free
- link: Book a Demo
- button: Missed Upsell
- button: Feature Gap Risk
- button: Bot Hallucination
- tab: Vercel AI SDK
- tab: TypeScript
- tab: Python
- tab: REST API
- button: Copy code to clipboard
- button: FAQ accordions (5)
- link: Get Started (per pricing tier)
- link: Contact Us (Enterprise)
- link: Footer links (Features, Pricing, FAQs, Docs, GitHub, Blog)

**Flows starting here:**
- [Navigate to login](flows/navigate-to-login.md) — Access the authentication page to log in to an existing OpenBat account from the public landing page.
- [Navigate to sign up](flows/navigate-to-sign-up.md) — Start the account creation process from the landing page to begin using OpenBat for chatbot analytics.
- [Explore features via anchor links](flows/explore-features-via-anchor-links.md) — Scroll through the landing page sections to learn about OpenBat's capabilities before signing up, using in-page anchor navigation.

---

### 2. Login Page (`/auth/login`)

Authentication page where existing users log in to their OpenBat account. Features a split layout with a login form on the left and a decorative image on the right. Supports email/password login and social authentication via Apple, Google, and Meta. Includes a link to the forgot password flow.

**Interactive elements:**
- textbox: Email
- textbox: Password
- button: Login
- button: Login with Apple
- button: Login with Google
- button: Login with Meta
- link: Forgot your password?
- link: Terms of Service
- link: Privacy Policy

**Flows starting here:**
- [Email login](flows/email-login.md) — Authenticate using email and password credentials to access the main dashboard. This is the primary authentication method for existing users.
- [Social auth login](flows/social-auth-login.md) — Authenticate using a third-party identity provider (Apple, Google, or Meta) for passwordless login.
- [Navigate to forgot password](flows/navigate-to-forgot-password.md) — Start the password reset process when a user has forgotten their credentials.

---

### 3. Sign Up Page (`/auth/sign-up`)

Account creation page for new users. Features a split layout with a registration form on the left and a decorative image on the right. Requires email, password, and password confirmation. Also supports social sign-up via Apple, Google, and Meta. Includes a link to sign in for existing users.

**Interactive elements:**
- textbox: Email
- textbox: Password
- textbox: Confirm Password
- button: Create Account
- button: Sign up with Apple
- button: Sign up with Google
- button: Sign up with Meta
- link: Sign in
- link: Terms of Service
- link: Privacy Policy

**Flows starting here:**
- [Email sign up](flows/email-sign-up.md) — Create a new OpenBat account using email and password. After sign-up, the user's organization is auto-created on first visit to the platform.

---

### 4. Forgot Password Page (`/auth/forgot-password`)

Password reset page where users enter their email to receive a reset link. Simple form with email input and submit button.

**Interactive elements:**
- textbox: Email
- button: Send reset email
- link: Login

**Flows starting here:**
- [Request password reset](flows/request-password-reset.md) — Submit an email address to receive a password reset link, allowing the user to regain access to their account.

---

### 5. Platform Dashboard — Chatbot List (`/platform`)

The main authenticated landing page showing all chatbots belonging to the user's organization. Displays chatbot cards with name, API key prefix, creator, creation date, conversation count, and message count. Supports filtering by status (Active, Pending, Archive) and switching between card and list views. Each chatbot card has a context menu (three-dot button) with Open chatbot, Archive, and Delete actions.

**Interactive elements:**
- button: New chatbot
- button: Active filter
- button: Pending filter
- button: Archive filter
- button: Card view
- button: List view
- button: chatbot context menu (per card)
- link: Chatbots (sidebar)
- link: Members (sidebar)
- link: Settings (sidebar)
- button: User account menu (sidebar footer)

**Flows starting here:**
- [Create new chatbot](flows/create-new-chatbot.md) — Add a new chatbot to the organization to begin capturing and analyzing conversations from a new AI assistant deployment.
- [Open chatbot dashboard](flows/open-chatbot-dashboard.md) — Navigate into a specific chatbot's analytics dashboard to view conversation data, sentiment trends, and insights.
- [Switch chatbot view mode](flows/switch-chatbot-view-mode.md) — Toggle between card view (visual cards with stats) and list view (compact table) for the chatbot list.
- [Filter chatbots by status](flows/filter-chatbots-by-status.md) — Filter the chatbot list to show only Active, Pending, or Archived chatbots.

---

### 6. Organization Members (`/platform/members`)

Manage team members who have access to the organization. Displays a table of members with their email, role (Owner, etc.), and join date. Includes an 'Invite member' button to add new team members.

**Interactive elements:**
- button: Invite member
- table: members list (Email, Role, Joined)

**Flows starting here:**
- [Invite team member](flows/invite-team-member.md) — Add a new member to the organization so they can access chatbot dashboards and analytics alongside the team.

---

### 7. Organization Settings (`/platform/settings`)

Manage organization-level settings including the organization display name and a danger zone for permanently deleting the organization and all its data.

**Interactive elements:**
- textbox: Organization name
- button: Save
- button: Delete organization

**Flows starting here:**
- [Rename organization](flows/rename-organization.md) — Change the display name of the organization that appears throughout the platform.
- [Delete organization](flows/delete-organization.md) — Permanently delete the organization and all associated chatbots, conversations, messages, and analytics data. This is an irreversible destructive action.

---

### 8. Chatbot Overview Dashboard (`/platform/[chatbotId]`)

Main analytics dashboard for a specific chatbot. Shows stat cards (Conversations, Messages, Avg Sentiment, Analyzed Today), date range picker, segment filter (by Plan), and two tabs: User Insights and Assistant Performance. User Insights tab includes: sentiment trend chart, top user frustrations table, most dissatisfied users with investigate links, support topics table, revenue signals (churn risk, buying signals, capability gaps), top intents chart, sentiment by segment, activity heatmap, and languages breakdown. Assistant Performance tab includes: behavior alerts table (Hallucinating, Dodging, Verbose, Redirecting with severity), resolution outcomes donut chart, quality flags table, and capability gaps table.

**Interactive elements:**
- button: Select date range
- combobox: Segment by (Plan)
- tab: User Insights
- tab: Assistant Performance
- link: Investigate (per dissatisfied user)
- link: sidebar nav (Dashboard, Workflows, Conversations, Deep Search, Organizations, Users, Analysis Config, Settings, Get Help)
- button: New report
- button: Create your first report

**Flows starting here:**
- [View user insights](flows/view-user-insights.md) — Review the User Insights tab to understand customer sentiment trends, frustration patterns, support topics, revenue signals, and user behavior over time.
- [View assistant performance](flows/view-assistant-performance.md) — Review the Assistant Performance tab to identify problematic bot behaviors, resolution rates, quality issues, and capability gaps.
- [Investigate dissatisfied user](flows/investigate-dissatisfied-user.md) — Click through from the 'Most dissatisfied users' section to view all conversations for a specific unhappy user, filtered by their email.
- [Filter by date range](flows/filter-by-date-range.md) — Change the date range for all dashboard analytics to focus on a specific time period.

---

### 9. Workflows (`/platform/[chatbotId]/workflows`)

Workflow automation page for creating alert and action workflows that trigger based on conversation analysis conditions. Has three tabs: Workflows (list of configured workflows), Runs (execution history), and Templates (pre-built workflow templates). Shows empty state with 'Create workflow' button when no workflows exist.

**Interactive elements:**
- button: Create workflow
- tab: Workflows
- tab: Runs
- tab: Templates

**Flows starting here:**
- [Create workflow](flows/create-workflow.md) — Set up an automated workflow that triggers alerts or actions when specific analysis conditions are met (e.g., negative sentiment detected, churn risk flagged).

---

### 10. Conversations List (`/platform/[chatbotId]/conversations`)

Paginated table of all conversations captured by this chatbot. Columns: User, Email, Organization, Messages, Sentiment (with colored badge and score), Language (flag), Plan, Last Message, Created. Supports text search, column sorting, filter button, view configuration, date range selection, and pagination (20 rows per page). Clicking a row navigates to the conversation detail page.

**Interactive elements:**
- textbox: Filter conversations...
- button: Filter
- button: View
- button: Select date range
- table: conversations (sortable columns)
- pagination: rows per page, page navigation

**Flows starting here:**
- [Browse conversations](flows/browse-conversations.md) — Browse, search, and filter all captured chatbot conversations to find specific interactions or patterns.

![Conversations List](screenshots/page-10.png)

---

### 11. Conversation Detail (`/platform/[chatbotId]/conversations/[conversationId]`)

Detailed view of a single conversation showing a chat-bubble interface with user and assistant messages in chronological order. Each message has timestamp, and analyzed messages show behavior/intent/sentiment badges (e.g., 'Dodging', 'Deflected', 'Helpful', 'conversational greeting'). Highlighted text spans within messages indicate detected patterns. Right sidebar shows: Overall Sentiment card, Conversation metadata (Messages, Conv ID, First/Last message, Created), User info (Name, Email, User ID), Organization info (Name, Org ID), Session info (Referrer, Device), Custom Metadata. Breadcrumb navigation back to conversations list. Filter and View buttons available.

**Interactive elements:**
- breadcrumb: Conversations > [User Name]
- button: Filter
- button: View
- button: message bubbles (clickable for analysis details)
- button: behavior badges (Dodging, Deflected, Helpful, etc.)
- button: intent badges (conversational greeting, etc.)
- sidebar: Overall Sentiment
- sidebar: Conversation metadata
- sidebar: User info
- sidebar: Organization info
- sidebar: Session info
- sidebar: Custom Metadata

**Flows starting here:**
- [Review conversation analysis](flows/review-conversation-analysis.md) — Read through a full conversation and examine the AI-generated analysis badges on each message to understand user sentiment, assistant behavior, and conversation outcomes.

---

### 12. Deep Search (`/platform/[chatbotId]/deep-search`)

Semantic search page that finds conversations by meaning rather than keywords. Features a search input with a placeholder example ('users asking about pricing' or 'billing issues'), a date range picker, and a 'Deep Search' button. Shows an empty state when no query has been entered.

**Interactive elements:**
- textbox: Search by meaning
- button: Deep Search
- button: Select date range

**Flows starting here:**
- [Semantic search conversations](flows/semantic-search-conversations.md) — Search for conversations using natural language queries that match by semantic meaning, not just keywords. For example, searching 'users frustrated with billing' would find conversations about payment issues even if the word 'billing' wasn't used.

![Deep Search](screenshots/page-12.png)

---

### 13. Client Organizations (`/platform/[chatbotId]/organizations`)

Paginated table of customer organizations that have interacted with the chatbot. Columns: Organization, Plan (demo/client), Industry, MRR, Conversations, Users, Sentiment (with colored badge), Last Activity. Supports text search, filtering, view configuration, column sorting, and date range selection. 48 rows with pagination.

**Interactive elements:**
- textbox: Filter organizations...
- button: Filter
- button: View
- button: Select date range
- table: organizations (sortable columns)
- pagination controls

**Flows starting here:**
- [Browse client organizations](flows/browse-client-organizations.md) — View all customer organizations that have used the chatbot, sorted and filtered to understand which organizations are most active, most dissatisfied, or generate the most conversations.

---

### 14. Chatbot Users (`/platform/[chatbotId]/users`)

Paginated table of individual users who have interacted with the chatbot. Columns: User, Email, Organization, Plan, MRR, Conversations, Sentiment (with colored badge and score), Last Activity. Supports text search, filtering, view configuration, column sorting, and date range selection. 26 rows with pagination.

**Interactive elements:**
- textbox: Filter users...
- button: Filter
- button: View
- button: Select date range
- table: users (sortable columns)
- pagination controls

**Flows starting here:**
- [Browse chatbot users](flows/browse-chatbot-users.md) — View all individual users who have conversed with the chatbot, with their aggregate sentiment scores and conversation counts, to identify specific users who need attention.

![Chatbot Users](screenshots/page-14.png)

---

### 15. Analysis Config (`/platform/[chatbotId]/analysis-config`)

Configuration page for how chatbot conversations are analyzed. Has five tabs: Metadata (managed fields and discovered fields with accept/deny/track controls), Translation, User Analysis, Assistant Analysis, and Prompts. The Metadata tab shows managed fields table (Key, Type, Status, Used, Discovered, Actions) and discovered fields table (Key, Sample value, Occurrences) with '+ Track' buttons to start tracking new metadata keys.

**Interactive elements:**
- tab: Metadata
- tab: Translation
- tab: User Analysis
- tab: Assistant Analysis
- tab: Prompts
- table: managed fields
- table: discovered fields
- button: Track (per discovered field)
- button: remove (per managed field)

**Flows starting here:**
- [Manage metadata fields](flows/manage-metadata-fields.md) — Accept, deny, or track custom metadata keys sent by the SDK to control which fields appear as filters in the conversations table.
- [Configure analysis settings](flows/configure-analysis-settings.md) — Switch between the five configuration tabs (Metadata, Translation, User Analysis, Assistant Analysis, Prompts) to fine-tune how the AI analyzes conversations.

---

### 16. Chatbot Settings (`/platform/[chatbotId]/settings`)

Comprehensive chatbot configuration page with six tabs: General (chatbot name, ID, creation date, message analysis toggles, delete chatbot), Company Info, API Keys, Members, Webhooks, Import/Export Data. The General tab includes toggles for enabling/disabling user and assistant message analysis, and a danger zone for permanently deleting the chatbot.

**Interactive elements:**
- tab: General
- tab: Company Info
- tab: API Keys
- tab: Members
- tab: Webhooks
- tab: Import/Export Data
- textbox: Chatbot name
- button: Save
- button: Copy chatbot ID
- switch: User message analysis
- switch: Assistant message analysis
- button: Delete chatbot

**Flows starting here:**
- [Rename chatbot](flows/rename-chatbot.md) — Change the display name of a chatbot that appears throughout the dashboard.
- [Toggle message analysis](flows/toggle-message-analysis.md) — Enable or disable automatic analysis for user messages and/or assistant messages to control which signals are extracted.
- [Delete chatbot](flows/delete-chatbot.md) — Permanently delete a chatbot and all its associated conversations, messages, and analytics data. This is irreversible.
- [Manage API keys](flows/manage-api-keys.md) — View, create, or rotate API keys used by the SDK to send conversation data to this chatbot.

![Chatbot Settings](screenshots/page-16.png)

---

### 17. Chatbot Onboarding (`/platform/[chatbotId]/onboarding`)

SDK setup instructions page shown after creating a new chatbot. Guides the user through installing and configuring the OpenBat SDK. If the chatbot is already onboarded (settings.onboarded = true), this page redirects back to the chatbot dashboard.

**Interactive elements:**
- SDK setup instructions
- Code snippets
- API key display

**Flows starting here:**
- [Complete chatbot onboarding](flows/complete-chatbot-onboarding.md) — Follow the SDK setup instructions to integrate OpenBat with an AI chatbot, then mark onboarding as complete to access the full dashboard.

![Chatbot Onboarding](screenshots/page-17.png)

---

## All Discovered Flows

- [Navigate to login](flows/navigate-to-login.md)
- [Navigate to sign up](flows/navigate-to-sign-up.md)
- [Explore features via anchor links](flows/explore-features-via-anchor-links.md)
- [Email login](flows/email-login.md)
- [Social auth login](flows/social-auth-login.md)
- [Navigate to forgot password](flows/navigate-to-forgot-password.md)
- [Email sign up](flows/email-sign-up.md)
- [Request password reset](flows/request-password-reset.md)
- [Create new chatbot](flows/create-new-chatbot.md)
- [Open chatbot dashboard](flows/open-chatbot-dashboard.md)
- [Switch chatbot view mode](flows/switch-chatbot-view-mode.md)
- [Filter chatbots by status](flows/filter-chatbots-by-status.md)
- [Invite team member](flows/invite-team-member.md)
- [Rename organization](flows/rename-organization.md)
- [Delete organization](flows/delete-organization.md)
- [View user insights](flows/view-user-insights.md)
- [View assistant performance](flows/view-assistant-performance.md)
- [Investigate dissatisfied user](flows/investigate-dissatisfied-user.md)
- [Filter by date range](flows/filter-by-date-range.md)
- [Create workflow](flows/create-workflow.md)
- [Browse conversations](flows/browse-conversations.md)
- [Review conversation analysis](flows/review-conversation-analysis.md)
- [Semantic search conversations](flows/semantic-search-conversations.md)
- [Browse client organizations](flows/browse-client-organizations.md)
- [Browse chatbot users](flows/browse-chatbot-users.md)
- [Manage metadata fields](flows/manage-metadata-fields.md)
- [Configure analysis settings](flows/configure-analysis-settings.md)
- [Rename chatbot](flows/rename-chatbot.md)
- [Toggle message analysis](flows/toggle-message-analysis.md)
- [Delete chatbot](flows/delete-chatbot.md)
- [Manage API keys](flows/manage-api-keys.md)
- [Complete chatbot onboarding](flows/complete-chatbot-onboarding.md)
