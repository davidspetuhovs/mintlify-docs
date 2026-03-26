# Sort by column

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Sort by column |
| **Starting Page** | Client Users |
| **URL** | `/platform/[chatbotId]/users` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity. Clicking a row filters conversations by that user

### Starting Page Screenshot

![Client Users](../screenshots/page-14.png)

## Business Purpose

This flow allows users to **sort by column** from the Client Users page.

## Related Flows (Same Page)

- [Browse users](browse-users.md)
- [Filter by user](filter-by-user.md)

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

### Step 2: Verify outcome

Verify that the "Sort by column" completed successfully and the expected state change occurred.

{{screenshot_2}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/users → [Sort by column]
```

## Related Pages

- **Conversations List** (`/platform/[chatbotId]/conversations`) — Paginated conversation table with sortable columns, search, filters, and date range. Supports filter
- **Client Organizations** (`/platform/[chatbotId]/organizations`) — Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last acti
