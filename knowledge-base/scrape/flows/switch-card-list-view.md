# Switch card/list view

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Switch card/list view |
| **Starting Page** | Dashboard - Chatbots List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pending/Archive), and new chatbot button

## Business Purpose

This flow allows users to **switch card/list view** from the Dashboard - Chatbots List page.

## Related Flows (Same Page)

- [Create new chatbot](create-new-chatbot.md)
- [Open chatbot](open-chatbot.md)
- [Archive chatbot](archive-chatbot.md)
- [Delete chatbot](delete-chatbot.md)
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

### Step 2: Interact with button: Card view

Use the **button: Card view** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: List view

Use the **button: List view** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Switch card/list view" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /platform → [Switch card/list view]
```
