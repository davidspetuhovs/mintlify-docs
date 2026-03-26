# Browse users

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Browse users |
| **Starting Page** | Client Users |
| **URL** | `/platform/[chatbotId]/users` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity. Clicking a row filters conversations by that user

### Starting Page Screenshot

![Client Users](../screenshots/page-14.png)

## Business Purpose

This flow allows users to **browse users** from the Client Users page.

## Related Flows (Same Page)

- [Filter by user](filter-by-user.md)
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

### Step 3: Verify outcome

Verify that the "Browse users" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/users → [Browse users]
```

## Related Pages

- **Client Organizations** (`/platform/[chatbotId]/organizations`) — Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last acti
