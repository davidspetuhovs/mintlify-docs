# Test Plan

## 1. Email Sign Up

**Preconditions:** No existing account for the test email.

- [ ] Navigate to `/auth/sign-up`
- [ ] Verify form fields: Work email, Password, Confirm password
- [ ] Enter valid work email, password (8+ chars), matching confirmation
- [ ] Click "Create account"
- [ ] Verify redirect to success/verification page
- [ ] Verify verification email is received

### Failure Modes
- [ ] Submit with mismatched passwords → expect inline validation error
- [ ] Submit with already-registered email → expect error message
- [ ] Submit with weak/short password → expect password policy error

---

## 2. Email Login

**Preconditions:** Verified account exists.

- [ ] Navigate to `/auth/login`
- [ ] Enter valid email and password
- [ ] Click sign-in button
- [ ] Verify redirect to `/platform` (chatbot list)
- [ ] Verify session is established (no redirect back to login)

### Failure Modes
- [ ] Enter incorrect password → expect authentication error

---

## 3. Password Reset Request

**Preconditions:** Account exists with verified email.

- [ ] Navigate to `/auth/forgot-password`
- [ ] Enter registered email
- [ ] Submit the form
- [ ] Verify confirmation message displayed
- [ ] Verify reset email received with valid link

### Failure Modes
- [ ] Enter unregistered email → expect graceful handling (no account enumeration)

---

## 4. Sign Up from Landing Page

**Preconditions:** None.

- [ ] Navigate to `/`
- [ ] Scroll through features section
- [ ] Locate and click "Start listening" CTA button
- [ ] Verify navigation to `/auth/sign-up`

### Failure Modes
- [ ] CTA button not visible or not clickable on mobile viewport

---

## 5. Create New Chatbot

**Preconditions:** Logged in, organization exists.

- [ ] Navigate to `/platform`
- [ ] Click "Create chatbot" button
- [ ] Enter chatbot name
- [ ] Confirm creation
- [ ] Verify redirect to onboarding page `/platform/[chatbotId]/onboarding`
- [ ] Verify API key is displayed and copyable

---

## 6. Chatbot Onboarding Wizard

**Preconditions:** New chatbot created, onboarding not completed.

- [ ] Verify onboarding page shows SDK setup instructions
- [ ] Copy API key
- [ ] Complete onboarding steps
- [ ] Verify redirect to chatbot dashboard after marking complete
- [ ] Verify revisiting onboarding redirects to dashboard if already onboarded

---

## 7. Explore Demo Chatbot

**Preconditions:** Logged in, demo chatbot exists.

- [ ] Navigate to `/platform`
- [ ] Switch to "Demo" tab
- [ ] Click on demo chatbot card
- [ ] Verify dashboard loads with sample data (read-only)

---

## 8. Invite Team Member

**Preconditions:** Logged in as Owner or Admin.

- [ ] Navigate to `/platform/members`
- [ ] Click invite button
- [ ] Fill in email, select organization role (Admin or Member)
- [ ] Configure chatbot access (select specific chatbots, set Editor/Viewer role)
- [ ] Click "Send invitation"
- [ ] Verify invitation appears in members list or pending state

---

## 9. Ask AI About Chatbot Data

**Preconditions:** Logged in, chatbot has conversation data.

- [ ] Navigate to `/platform/[chatbotId]`
- [ ] Type a natural-language question in the AI chat input
- [ ] Submit the message
- [ ] Verify AI response appears with relevant data

### Failure Modes
- [ ] Submit empty message → expect no submission or validation message

---

## 10. Create Report from Template

**Preconditions:** Logged in, chatbot exists.

- [ ] Navigate to `/platform/[chatbotId]/reports`
- [ ] Click a template card (e.g., "Customer Pulse")
- [ ] Verify report is created and opened
- [ ] Verify AI-generated widgets render

---

## 11. Create Workflow from Template

**Preconditions:** Logged in, chatbot exists.

- [ ] Navigate to `/platform/[chatbotId]/workflows`
- [ ] Switch to "Templates" tab
- [ ] Select a template (e.g., from Alerting category)
- [ ] Verify workflow is created and appears in Workflows tab

---

## 12. Create New Prompt Version

**Preconditions:** Logged in, chatbot exists with system prompt.

- [ ] Navigate to `/platform/[chatbotId]/system-prompt`
- [ ] Verify Prompt tab is active
- [ ] Edit the prompt text
- [ ] Click publish/save
- [ ] Verify new version appears in timeline

---

## 13. Review a Specific Conversation

**Preconditions:** Chatbot has conversation data.

- [ ] Navigate to `/platform/[chatbotId]/conversations`
- [ ] Click on a conversation row
- [ ] Verify transcript loads with user (pink) and assistant (green) message bubbles
- [ ] Verify General, User, and Assistant analysis tabs are present and populated

---

## 14. Configure Analysis Definitions

**Preconditions:** Logged in, chatbot exists.

- [ ] Navigate to `/platform/[chatbotId]/analysis-config`
- [ ] Switch between tabs: Integration, Metadata, Translation, User Analysis, Assistant Analysis, Calibration, Personas
- [ ] Modify a setting (e.g., toggle auto-translate, add a custom flag)
- [ ] Verify changes persist after page reload

---

## 15. Export Conversation Data

**Preconditions:** Chatbot has conversation data.

- [ ] Navigate to `/platform/[chatbotId]/settings`
- [ ] Switch to "Import/Export Data" tab
- [ ] Click export (JSON or CSV)
- [ ] Verify file downloads with expected data

---

## 16. Conversation List Filtering & Pagination

**Preconditions:** Chatbot has 50+ conversations.

- [ ] Navigate to `/platform/[chatbotId]/conversations`
- [ ] Use text search filter
- [ ] Apply faceted filters (sentiment, outcome, flags)
- [ ] Apply date range filter
- [ ] Sort by different columns
- [ ] Navigate to page 2+
- [ ] Verify all filters combine correctly

---

## 17. Deep Search

**Preconditions:** Chatbot has conversation data.

- [ ] Navigate to `/platform/[chatbotId]/deep-search`
- [ ] Enter a semantic query (e.g., "frustrated users asking about billing")
- [ ] Click "Deep Search"
- [ ] Verify results returned are semantically relevant

---

## 18. Organization Settings

**Preconditions:** Logged in as Owner.

- [ ] Navigate to `/platform/settings`
- [ ] Edit organization name → save → verify persisted
- [ ] Verify danger zone (delete organization) is visible with confirmation gate

---

## 19. Chatbot Settings Tabs

**Preconditions:** Logged in, chatbot exists.

- [ ] Navigate to `/platform/[chatbotId]/settings`
- [ ] Verify all 7 tabs load: General, Billing, Company Info, API Keys, Members, Webhooks, Import/Export Data
- [ ] General: verify name edit, analysis toggles, delete button
- [ ] API Keys: verify key prefix displayed, rotate functionality
- [ ] Webhooks: verify Discord/Slack/custom webhook configuration