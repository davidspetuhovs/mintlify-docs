# Create new chatbot

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Create new chatbot |
| **Starting Page** | Dashboard - Chatbots List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pending/Archive), and new chatbot button

## Business Purpose

This flow allows users to **create new chatbot** from the Dashboard - Chatbots List page.

## Related Flows (Same Page)

- [Open chatbot](open-chatbot.md)
- [Archive chatbot](archive-chatbot.md)
- [Delete chatbot](delete-chatbot.md)
- [Switch card/list view](switch-card-list-view.md)
- [Filter by status](filter-by-status.md)
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

### Step 2: Interact with button: New chatbot

Use the **button: New chatbot** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: chatbot context menu (Open/Archive/Delete)

Use the **button: chatbot context menu (Open/Archive/Delete)** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with link: Chatbots

Use the **link: Chatbots** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "Create new chatbot" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform → [Create new chatbot]
```

## Related Pages

- **Workflows** (`/platform/[chatbotId]/workflows`) — Workflow automation page with Workflows/Runs/Templates tabs
