# Filter by user

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter by user |
| **Starting Page** | Client Users |
| **URL** | `/platform/[chatbotId]/users` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity. Clicking a row filters conversations by that user

### Starting Page Screenshot

![Client Users](../screenshots/page-14.png)

## Business Purpose

This flow allows users to **filter by user** from the Client Users page.

## Related Flows (Same Page)

- [Browse users](browse-users.md)
- [Sort by column](sort-by-column.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Filter users
- button: Filter
- button: View
- button: date range
- table: User/Email/Organization/Plan/MRR/Conversations/Sentiment/Last Activity
- pagination controls

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/users` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with textbox: Filter users

Use the **textbox: Filter users** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Filter

Use the **button: Filter** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with table: User/Email/Organization/Plan/MRR/Conversations/Sentiment/Last Activity

Use the **table: User/Email/Organization/Plan/MRR/Conversations/Sentiment/Last Activity** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "Filter by user" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/users → [Filter by user]
```

## Related Pages

- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Conversations List** (`/platform/[chatbotId]/conversations`) — Paginated conversation table with sortable columns, search, filters, and date range. Supports filter
- **Client Organizations** (`/platform/[chatbotId]/organizations`) — Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last acti
