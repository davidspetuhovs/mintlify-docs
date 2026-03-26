# Screenshot Guide

This document maps every screenshot used in the OpenBat docs to its file location, usage context, and what the replacement screenshot should show.

Once you create a replacement screenshot, drop it into `/images/` with the same filename and it will automatically appear in the docs.

---

## 1. `landing.png`

**File path:** `/images/landing.png`

**Used in:**
- `guides/introduction.mdx` (line 10) — hero image at the top of the "What is OpenBat" page

**What it currently shows:** The OpenBat marketing landing page with the headline "Google Analytics for AI chatbots" and a small preview of the dashboard in the corner.

**What it should show:** A polished overview of the OpenBat platform in action — ideally the dashboard with real-looking data (sentiment charts, conversation counts, behavior alerts). This is the first image new users see, so it should communicate "analytics platform for chatbot teams" at a glance. Think: a clean dashboard screenshot with visible metrics, charts, and sidebar navigation — not the marketing site itself.

---

## 2. `sign-up.png`

**File path:** `/images/sign-up.png`

**Used in:**
- `guides/quickstart.mdx` (line 15) — Step 1 "Create an account"

**What it currently shows:** The account creation form with email, password, confirm password fields, "Create Account" button, and social login options (Apple, Google, passkey). The right half of the card shows a broken image placeholder.

**What it should show:** A clean screenshot of the sign-up page with no broken images. The form should be empty (placeholder state) or have example data filled in. Make sure the right panel either loads correctly or is cropped out. The social login buttons and "Already have an account?" link should be visible.

---

## 3. `chatbots-list.png`

**File path:** `/images/chatbots-list.png`

**Used in:**
- `guides/quickstart.mdx` (line 25) — Step 2 "Create a chatbot"

**What it currently shows:** The chatbots list in table view with 2 chatbots ("support bot" and "test"), showing the sidebar with org name "Test", and the "New chatbot" button.

**What it should show:** The chatbots page with at least 1-2 chatbots visible, the "+ New chatbot" button clearly visible in the top right, and chatbot cards/rows showing conversation and message counts. Ideally use the card view (grid layout) since it looks more visual. Use realistic chatbot names (e.g., "Customer Support Bot", "Sales Assistant") instead of "test".

---

## 4. `dashboard.png`

**File path:** `/images/dashboard.png`

**Used in:**
- `guides/quickstart.mdx` (line 71) — Step 5 "View your dashboard"
- `guides/dashboard.mdx` (line 6) — hero image for the Dashboard guide

**What it currently shows:** The dashboard with the greeting "Good morning, test", overview strip (373 conversations, 1,292 messages, 0 neutral sentiment, 0 resolution), the User Insights tab selected, and a "User sentiment" chart that's mostly empty/hard to read.

**What it should show:** A dashboard populated with realistic data that demonstrates the platform's value:
- Overview strip with meaningful numbers and trend arrows (e.g., 1,247 conversations, +12% trend)
- A visible sentiment score (e.g., "Positive 0.42") with a trend indicator
- Resolution rate with a percentage
- The User Analytics tab showing a populated sentiment bands chart
- The dissatisfied users list and top frustrations visible below
- Use a realistic greeting name, not "test"

**Note:** This image is used in TWO places. It needs to work both as a quickstart "here's what you'll see" preview AND as the dashboard guide hero. A well-populated dashboard with all key sections visible covers both.

---

## 5. `conversations-list.png`

**File path:** `/images/conversations-list.png`

**Used in:**
- `guides/conversations.mdx` (line 10) — top of the "Conversation list" section

**What it currently shows:** The conversations table with columns for user, organization, messages, sentiment, language, and dates. Shows ~8 rows of conversation data with user names and org names. The sidebar shows full navigation.

**What it should show:** A well-populated conversations table with:
- Clear column headers (User, Organization, Messages, Sentiment, Language, Last active, Started)
- Sentiment badges in different colors (mix of positive, neutral, negative)
- A visible search bar and filter controls at the top
- At least 8-10 rows of realistic data
- Pagination controls at the bottom
- The current screenshot is decent but ensure sentiment badges are clearly color-coded and the filter bar is visible

---

## 6. `conversation-detail.png`

**File path:** `/images/conversation-detail.png`

**Used in:**
- `guides/conversations.mdx` (line 61) — top of the "Conversation detail" section

**What it currently shows:** A conversation detail view showing a conversation with "Tech JHorizon" — the message transcript is visible with user and assistant messages, but the analysis badges (sentiment, intent, topics, behaviors) are hard to read at this resolution.

**What it should show:** A conversation detail view that clearly demonstrates the analysis overlays:
- The conversation header with user name, org, message count, and average sentiment
- A breadcrumb navigation back to the conversations list
- At least 2-3 message pairs (user + assistant)
- Clearly visible analysis badges on user messages: sentiment (colored), intent, topic tags
- Clearly visible analysis badges on assistant messages: behavior, outcome
- Consider zooming in or using a larger resolution so the badges are legible

---

## 7. `deep-search.png`

**File path:** `/images/deep-search.png`

**Used in:**
- `guides/deep-search.mdx` (line 8) — hero image for the Deep Search guide

**What it currently shows:** The deep search page in its empty/initial state — search bar with placeholder text, "Enter a query to start searching" message, and the sparkle icon.

**What it should show:** The deep search page WITH search results visible. Show:
- A natural language query typed in the search bar (e.g., "users frustrated about billing")
- Search results table with User, Message (truncated), Sentiment badge, Conversation link, and Date columns
- At least 4-5 result rows showing semantically matched messages
- The current empty state screenshot doesn't demonstrate the feature's value

---

## 8. `users.png`

**File path:** `/images/users.png`

**Used in:**
- `guides/users-and-organizations.mdx` (line 12) — inside the "Users" tab

**What it currently shows:** The users table with columns for user name/email, organization, conversations count, avg sentiment, and other fields. Shows ~8 rows of user data. The "This month" filter is visible.

**What it should show:** The users directory with:
- Visible column headers: User, Plan, Industry, Organization, Conversations, Avg Sentiment, MRR, First seen
- Filter controls and search bar at the top
- Mix of sentiment values (some green/positive, some red/negative)
- Realistic user data with varied plans and industries
- The current screenshot is reasonable but ensure the Plan, Industry, and MRR columns are visible since the docs describe them

---

## 9. `organizations.png`

**File path:** `/images/organizations.png`

**Used in:**
- `guides/users-and-organizations.mdx` (line 49) — inside the "Organizations" tab

**What it currently shows:** The organizations table with org names, plan, industry, users count, conversations, sentiment, and other columns. Shows ~10 rows. A "Net Negative" red badge is visible on one row.

**What it should show:** The organizations table with:
- Clear column headers: Organization, Plan, Industry, Users, Conversations, Avg Sentiment, MRR, First seen
- Filter controls and search bar
- A mix of sentiment badges (positive, neutral, negative)
- Realistic org names and varied data
- The current screenshot is decent — just ensure all documented columns are visible and the sentiment badges are clear

---

## 10. `workflows.png`

**File path:** `/images/workflows.png`

**Used in:**
- `guides/workflows.mdx` (line 8) — hero image for the Workflows guide

**What it currently shows:** The workflows page — hard to read at this resolution, but appears to show the workflow list or creation interface.

**What it should show:** The workflow creation/list page showing:
- At least 1-2 existing workflows with their names, trigger types, and enabled/disabled status
- The "Create workflow" button
- Ideally show a workflow in expanded/edit view demonstrating the trigger → conditions → actions chain
- OR show the workflow builder with a condition like "sentiment < -0.5 AND flag = churn_risk" and a Slack action configured

---

## 11. `chatbot-settings.png`

**File path:** `/images/chatbot-settings.png`

**Used in:**
- `guides/settings.mdx` (line 10) — hero image for the Settings guide

**What it currently shows:** The settings page General tab showing chatbot name ("test"), chatbot ID, and creation date. The tab bar shows General, Company Info, API Keys, Metadata, Webhooks, Import/Export Data.

**What it should show:** The settings page with:
- A realistic chatbot name (not "test")
- The General tab active showing the name field, API key (masked), and rotate/delete options
- The tab navigation visible: General, Metadata, Webhooks, Access
- Note: the current tab names in the screenshot (Company Info, API Keys, Import/Export Data) don't match what the docs describe (General, Metadata, Webhooks, Access) — this suggests the UI has changed or the screenshot is outdated

---

## 12. `org-members.png`

**File path:** `/images/org-members.png`

**Used in:**
- `guides/team-management.mdx` (line 44) — after the "Inviting members" steps

**What it currently shows:** The organization dashboard sidebar with "Chatbots", "Members", "Settings" navigation. Shows the chatbots list with context menu (Open chatbot, Archive, Delete) open on one chatbot card.

**What it should show:** The Members page (not the chatbots page). It should show:
- The members list/table with columns for name, email, and role
- At least 2-3 team members with different roles (Owner, Admin, Member)
- The "Invite member" button visible
- The current screenshot is completely wrong — it shows the chatbots list with a context menu, not the members page at all

---

## 13. `org-settings.png`

**File path:** `/images/org-settings.png`

**Used in:**
- `guides/team-management.mdx` (line 54) — under "Organization settings"

**What it currently shows:** The chatbots list page again (same as chatbots-list.png but in table view), not the organization settings page.

**What it should show:** The organization settings page with:
- Organization name field (editable)
- The rename/save functionality
- The delete organization section with its warning
- This screenshot is also completely wrong — it shows the chatbots list, not org settings

---

## 14. `analysis-config.png`

**File path:** `/images/analysis-config.png`

**Used in:**
- `guides/analysis-configuration.mdx` (line 6) — hero image for the Analysis Configuration guide

**What it currently shows:** The analysis config page showing what appears to be the Metadata tab — managed fields table with key/type/discovered columns, and a "Discovered fields" section below.

**What it should show:** The analysis configuration page showing:
- The User Analysis or Assistant Analysis tab
- Toggle switches for each analysis type (Sentiment, Intent, Topic, Flag)
- An expanded section showing intent or topic definitions (slug, display name, description)
- The "Generate Definitions" button
- The current screenshot appears to show the metadata/managed fields section, not the analysis configuration toggles and definitions

---

## 15. `user-menu.png` (UNUSED)

**File path:** `/images/user-menu.png`

**Used in:** Not referenced in any documentation file.

**What it currently shows:** The chatbots list in table view with the user menu dropdown open at the bottom-left corner, showing the user's name/email, "Settings", and "Log out" options.

**What to do:** This image is currently unused. It could be useful for:
- A "Getting started" or "Navigation" guide explaining the user menu
- The team management page to show where users access their profile/settings
- Can be deleted if no docs page needs it

---

## Pages Missing Screenshots

### `guides/reports.mdx`
**Should have:** A screenshot of a populated custom report showing:
- The report name at the top
- A grid of widgets: stat widgets (conversation count, sentiment, resolution rate) in a row of thirds
- Chart widgets (sentiment trend line chart, conversation volume bar chart) at half width
- A list widget (top topics or recent conversations) at full width
- The time range selector in the top right

### `guides/translation.mdx`
**Could have:** A screenshot showing:
- A conversation detail view with translated messages
- The "Translated from [language]" indicator visible on a message
- The translation toggle in the filter bar
- Before/after of original vs translated text

---

## Summary

| # | Image | Status | Action Needed |
|---|-------|--------|---------------|
| 1 | `landing.png` | Wrong content | Replace with actual dashboard screenshot, not marketing site |
| 2 | `sign-up.png` | Broken | Fix broken image on right panel, or crop it out |
| 3 | `chatbots-list.png` | Okay | Use realistic names instead of "test" |
| 4 | `dashboard.png` | Underpopulated | Populate with realistic data, fix "test" greeting |
| 5 | `conversations-list.png` | Okay | Ensure sentiment badges and filters are clearly visible |
| 6 | `conversation-detail.png` | Low resolution | Re-capture at higher resolution so analysis badges are legible |
| 7 | `deep-search.png` | Empty state | Replace with a screenshot showing actual search results |
| 8 | `users.png` | Okay | Ensure all documented columns (Plan, MRR) are visible |
| 9 | `organizations.png` | Okay | Minor cleanup, ensure all columns visible |
| 10 | `workflows.png` | Low resolution | Re-capture showing workflow builder or list clearly |
| 11 | `chatbot-settings.png` | Possibly outdated | Tab names don't match docs — re-capture current UI |
| 12 | `org-members.png` | WRONG screenshot | Currently shows chatbots list — needs to show Members page |
| 13 | `org-settings.png` | WRONG screenshot | Currently shows chatbots list — needs to show Org Settings page |
| 14 | `analysis-config.png` | Wrong section | Shows metadata fields, not analysis config toggles/definitions |
| 15 | `user-menu.png` | Unused | Delete or find a home for it |
| -- | (reports) | MISSING | New screenshot needed for `guides/reports.mdx` |
| -- | (translation) | MISSING | New screenshot recommended for `guides/translation.mdx` |
