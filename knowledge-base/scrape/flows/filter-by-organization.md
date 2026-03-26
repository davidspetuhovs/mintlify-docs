# Filter by organization

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter by organization |
| **Starting Page** | Client Organizations |
| **URL** | `/platform/[chatbotId]/organizations` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last activity. Clicking a row filters conversations by that org

### Starting Page Screenshot

![Client Organizations](../screenshots/page-13.png)

## Business Purpose

This flow allows users to **filter by organization** from the Client Organizations page.

## Related Flows (Same Page)

- [Browse organizations](browse-organizations.md)
- [Sort by column](sort-by-column.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Filter organizations
- button: Filter
- button: View
- button: date range
- table: Organization/Plan/Industry/MRR/Conversations/Users/Sentiment/Last Activity
- pagination controls

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/organizations` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with textbox: Filter organizations

Use the **textbox: Filter organizations** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Filter

Use the **button: Filter** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with table: Organization/Plan/Industry/MRR/Conversations/Users/Sentiment/Last Activity

Use the **table: Organization/Plan/Industry/MRR/Conversations/Users/Sentiment/Last Activity** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "Filter by organization" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/organizations → [Filter by organization]
```

## Related Pages

- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Conversations List** (`/platform/[chatbotId]/conversations`) — Paginated conversation table with sortable columns, search, filters, and date range. Supports filter
- **Client Users** (`/platform/[chatbotId]/users`) — Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity.
