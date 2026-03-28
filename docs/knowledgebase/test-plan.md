# Test Plan — OpenBat

## 1. Authentication

### 1.1 Email Login
**Preconditions:** User has an existing account.
- [ ] Navigate to `/auth/login`
- [ ] Enter valid email in the Email field
- [ ] Enter valid password in the Password field
- [ ] Click the login/submit button
- [ ] Verify redirect to `/platform` dashboard

**Failure: Invalid credentials**
- [ ] Enter incorrect password
- [ ] Verify error message is displayed
- [ ] Verify user remains on login page

### 1.2 Social Auth Login
**Preconditions:** User has linked social account.
- [ ] Navigate to `/auth/login`
- [ ] Click Apple, Google, or Meta social auth button
- [ ] Verify OAuth redirect and successful authentication

**Failure: Social auth denial**
- [ ] Cancel or deny the OAuth prompt
- [ ] Verify graceful return to login page with appropriate message

### 1.3 Email Sign Up
**Preconditions:** None.
- [ ] Navigate to `/auth/sign-up`
- [ ] Enter email, password, and confirm password
- [ ] Submit the form
- [ ] Verify account creation and redirect

**Failure: Password mismatch**
- [ ] Enter different values in Password and Confirm Password
- [ ] Verify validation error is shown

**Failure: Duplicate email**
- [ ] Enter an email already associated with an account
- [ ] Verify appropriate error message

**Failure: Weak password**
- [ ] Enter a password that doesn't meet requirements
- [ ] Verify validation feedback

### 1.4 Password Reset
**Preconditions:** User has an existing account.
- [ ] Navigate to `/auth/login`
- [ ] Click "Forgot password" link
- [ ] Verify navigation to `/auth/forgot-password`
- [ ] Enter email and submit
- [ ] Verify confirmation message about reset email sent

### 1.5 Navigate to Sign Up from Landing
**Preconditions:** None.
- [ ] Navigate to `/`
- [ ] Find and click the sign-up link/button
- [ ] Verify navigation to `/auth/sign-up`

**Failure: Link not found**
- [ ] Verify sign-up CTA is visible without scrolling or is in header

---

## 2. Dashboard & Chatbot Management

### 2.1 Create a New Chatbot
**Preconditions:** User is logged in.
- [ ] Navigate to `/platform`
- [ ] Click "Create chatbot" button
- [ ] Verify modal appears with name field and character count (0/100)
- [ ] Enter chatbot name
- [ ] Click "Continue to setup"
- [ ] Verify chatbot appears in the list

### 2.2 Open a Chatbot
**Preconditions:** At least one chatbot exists.
- [ ] Navigate to `/platform`
- [ ] Verify chatbot cards display name, API key prefix, creator, last activity, conversation count, message count
- [ ] Click on a chatbot card
- [ ] Verify navigation to `/platform/{chatbotId}`
- [ ] Verify KPI cards load (Conversations, Messages, Avg Sentiment, Analyzed Today)

### 2.3 Filter Chatbots by Status
**Preconditions:** Chatbots exist in different statuses.
- [ ] Navigate to `/platform`
- [ ] Click "Active" tab — verify only active chatbots shown
- [ ] Click "Pending" tab — verify only pending chatbots shown
- [ ] Click "Archive" tab — verify only archived chatbots shown

### 2.4 Switch Organization
**Preconditions:** User belongs to multiple organizations.
- [ ] Click the organization switcher in the sidebar
- [ ] Select a different organization
- [ ] Verify dashboard updates to show that organization's chatbots

**Failure: Single org user**
- [ ] Verify switcher still renders gracefully (disabled or shows current org only)

---

## 3. Organization Management

### 3.1 Invite a Team Member
**Preconditions:** User is org owner/admin.
- [ ] Navigate to `/platform/members`
- [ ] Click invite button
- [ ] Verify invite modal with Email field and Role dropdown (Admin/Member)
- [ ] Enter email and select role
- [ ] Click "Invite"
- [ ] Verify new member appears in table (or pending invite shown)

### 3.2 Rename Organization
**Preconditions:** User is org owner.
- [ ] Navigate to `/platform/settings`
- [ ] Change the organization name field
- [ ] Save changes
- [ ] Verify name updates in sidebar/header

### 3.3 Delete Organization
**Preconditions:** User is org owner.
- [ ] Navigate to `/platform/settings`
- [ ] Locate danger zone
- [ ] Initiate deletion (expect confirmation step)
- [ ] Confirm deletion
- [ ] Verify organization and all data are removed

---

## 4. Chatbot Analytics

### 4.1 Change Analysis Time Period
**Preconditions:** Chatbot has conversation data.
- [ ] Navigate to `/platform/{chatbotId}`
- [ ] Click date range selector
- [ ] Select a new date range
- [ ] Verify KPI cards and charts update

### 4.2 View User Insights Tab
**Preconditions:** Chatbot has analyzed conversations.
- [ ] Navigate to `/platform/{chatbotId}`
- [ ] Click "User Insights" tab
- [ ] Verify sections: sentiment trends, top frustrations, dissatisfied users, support topics, revenue signals, top intents, sentiment by segment, activity heatmap, languages

### 4.3 View Assistant Performance Tab
- [ ] Click "Assistant Performance" tab
- [ ] Verify sections: behavior alerts, resolution outcomes donut chart, quality flags table, capability gaps

### 4.4 Investigate a Dissatisfied User
**Preconditions:** Dissatisfied users exist in data.
- [ ] On User Insights tab, find "Most Dissatisfied Users" section
- [ ] Click "Investigate" link on a user
- [ ] Verify navigation to conversation detail or filtered conversation list

**Failure: No dissatisfied users**
- [ ] Verify empty state or informative message

---

## 5. Conversations

### 5.1 View Conversation Detail
**Preconditions:** Conversations exist.
- [ ] Navigate to `/platform/{chatbotId}/conversations`
- [ ] Click on a conversation row
- [ ] Verify navigation to `/platform/{chatbotId}/conversations/{conversationId}`
- [ ] Verify breadcrumb navigation back to list
- [ ] Verify message thread with analysis annotations (sentiment, behavior flags, quality flags, resolution status)
- [ ] Verify right sidebar: Overall Sentiment, Conversation metadata, User info, Organization info, Session info

### 5.2 Filter Conversations
- [ ] Use search field to filter by keyword
- [ ] Verify table updates to show matching results
- [ ] Toggle column visibility using View button
- [ ] Sort by different columns
- [ ] Change date range filter
- [ ] Paginate through results

### 5.3 Review Message-Level Analysis
- [ ] Open a conversation detail
- [ ] Click on highlighted analysis annotations
- [ ] Verify clickable tags show details (sentiment, behavior, quality, resolution)

### 5.4 Semantic Deep Search
**Preconditions:** Conversations exist with varied content.
- [ ] Navigate to `/platform/{chatbotId}/deep-search`
- [ ] Enter a natural language query (e.g., "users asking about pricing")
- [ ] Click "Deep Search"
- [ ] Verify semantically relevant results are returned
- [ ] Adjust date range and search again

---

## 6. Workflows

### 6.1 Create Workflow from Template
- [ ] Navigate to `/platform/{chatbotId}/workflows`
- [ ] Click "Templates" tab
- [ ] Verify 6 templates visible (Alerting, Escalation, Reporting, Moderation, General)
- [ ] Click on a template
- [ ] Verify workflow is created or setup flow begins

### 6.2 Create Workflow from Scratch
- [ ] Click "Workflows" tab
- [ ] Click create button
- [ ] Enter workflow name, conditions, and actions
- [ ] Save the workflow
- [ ] Verify it appears in the workflows list

### 6.3 View Workflow Runs
- [ ] Click "Runs" tab
- [ ] Verify execution history table
- [ ] Filter by status: All, Pending, Triggered, Skipped, Success, Failed
- [ ] Verify correct filtering

---

## 7. Client Management

### 7.1 Browse Client Organizations
- [ ] Navigate to `/platform/{chatbotId}/organizations`
- [ ] Verify table columns: name, plan, industry, MRR, conversations, users, avg sentiment, last activity
- [ ] Use search to filter
- [ ] Sort by different columns
- [ ] Toggle column visibility

### 7.2 Browse Chatbot Users
- [ ] Navigate to `/platform/{chatbotId}/users`
- [ ] Verify table columns: name, email, organization, plan, MRR, conversations, sentiment, last activity
- [ ] Search, sort, and paginate

---

## 8. Analysis Configuration

### 8.1 Configure User Analysis Flags
- [ ] Navigate to `/platform/{chatbotId}/analysis-config`
- [ ] Click "User Analysis" tab
- [ ] Toggle sentiment scoring on/off
- [ ] Enable/disable predefined flags (Churn Risk, Frustrated User, etc.)
- [ ] Create a custom flag
- [ ] Verify changes persist

### 8.2 Enable Auto-Translation
- [ ] Click "Translation" tab
- [ ] Toggle auto-translate on
- [ ] Select a primary language
- [ ] Verify setting saves

### 8.3 Edit Analysis Prompts
- [ ] Click "Prompts" tab
- [ ] Edit the Sentiment analysis prompt
- [ ] Verify "Default" label present on unmodified prompts
- [ ] Save changes

### 8.4 Track Metadata Fields
- [ ] Click "Metadata" tab
- [ ] Verify discovered metadata fields from SDK
- [ ] Click Track/Accept on a field
- [ ] Click Deny on a field
- [ ] Verify status updates

### 8.5 Configure Assistant Analysis
- [ ] Click "Assistant Analysis" tab
- [ ] Toggle behavior classification flags (Helpful, Yes-Man, Dodging, Hallucinating, etc.)
- [ ] Verify changes persist

---

## 9. Chatbot Settings

### 9.1 View and Rotate API Keys
- [ ] Navigate to `/platform/{chatbotId}/settings`
- [ ] Click "API Keys" tab
- [ ] Verify masked API key displayed
- [ ] Copy API key
- [ ] Click rotate — verify confirmation and new key issued

### 9.2 Configure Webhooks
- [ ] Click "Webhooks" tab
- [ ] Click "Add webhook"
- [ ] Configure destination (Discord, Slack, or custom)
- [ ] Save and verify webhook appears in list

### 9.3 Export Conversation Data
- [ ] Click "Import/Export Data" tab
- [ ] Click export as JSON
- [ ] Toggle "include analysis results" option
- [ ] Verify download initiates

### 9.4 Import Conversation Data
- [ ] Click import option
- [ ] Download template
- [ ] Upload a JSON/CSV file
- [ ] Verify import processes

### 9.5 Manage Chatbot Members
- [ ] Click "Members" tab
- [ ] Click "Add member"
- [ ] Verify member is added to chatbot-level access

---

## 10. Landing Page

### 10.1 Explore Feature Demos
- [ ] Navigate to `/`
- [ ] Interact with animated chat widget demo
- [ ] Toggle between code integration examples (Vercel AI SDK, TypeScript, Python, REST API)
- [ ] Verify each tab shows relevant code snippet

### 10.2 Pricing Section
- [ ] Scroll to pricing section
- [ ] Verify Free through Enterprise tiers are visible
- [ ] Verify FAQ accordion expands/collapses

### 10.3 Responsive/Visual
- [ ] Verify AI provider logos carousel renders
- [ ] Verify testimonials section loads
- [ ] Verify CTA footer links work