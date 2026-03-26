# Filter conversations

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter conversations |
| **Starting Page** | Conversations List |
| **URL** | `/platform/[chatbotId]/conversations` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Paginated conversation table with sortable columns, search, filters, and date range. Supports filtering by user or org via query params

### Starting Page Screenshot

![Conversations List](../screenshots/page-10.png)

## Business Purpose

This flow allows users to **filter conversations** from the Conversations List page.

## Related Flows (Same Page)

- [Search conversations](search-conversations.md)
- [Sort by column](sort-by-column.md)
- [Navigate to conversation detail](navigate-to-conversation-detail.md)
- [Change page](change-page.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Filter conversations
- button: Filter
- button: View
- button: date range
- table: User/Email/Organization/Messages/Sentiment/Language/Plan/Last Message/Created
- pagination controls
- combobox: rows per page

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/conversations` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with textbox: Filter conversations

Use the **textbox: Filter conversations** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Filter

Use the **button: Filter** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Filter conversations" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/conversations → [Filter conversations]
```

## Related Pages

- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Client Organizations** (`/platform/[chatbotId]/organizations`) — Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last acti
- **Client Users** (`/platform/[chatbotId]/users`) — Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity.
