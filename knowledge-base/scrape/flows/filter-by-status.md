# Filter by status

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter by status |
| **Starting Page** | Dashboard - Chatbots List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pending/Archive), and new chatbot button

## Business Purpose

This flow allows users to **filter by status** from the Dashboard - Chatbots List page.

## Related Flows (Same Page)

- [Create new chatbot](create-new-chatbot.md)
- [Open chatbot](open-chatbot.md)
- [Archive chatbot](archive-chatbot.md)
- [Delete chatbot](delete-chatbot.md)
- [Switch card/list view](switch-card-list-view.md)
- [Log out](log-out.md)

## Available UI Elements

The following interactive elements are available on this page:

- button: New chatbot
- button: Active/Pending/Archive tabs
- button: Card view
- button: List view
- button: chatbot context menu (Open/Archive/Delete)
- link: Chatbots
- link: Members
- link: Settings
- button: user profile dropdown (Settings, Log out)

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform` and verify the page loads correctly.

### Step 2: Verify outcome

Verify that the "Filter by status" completed successfully and the expected state change occurred.

{{screenshot_2}}

## Navigation Path

```
http://localhost:3000 → /platform → [Filter by status]
```

## Related Pages

- **Conversations List** (`/platform/[chatbotId]/conversations`) — Paginated conversation table with sortable columns, search, filters, and date range. Supports filter
- **Client Organizations** (`/platform/[chatbotId]/organizations`) — Table of customer organizations with plan, industry, MRR, conversations, users, sentiment, last acti
- **Client Users** (`/platform/[chatbotId]/users`) — Table of chatbot users with email, organization, plan, MRR, conversations, sentiment, last activity.
