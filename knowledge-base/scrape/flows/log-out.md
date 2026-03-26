# Log out

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Log out |
| **Starting Page** | Dashboard - Chatbots List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pending/Archive), and new chatbot button

## Business Purpose

This flow allows users to **log out** from the Dashboard - Chatbots List page.

## Related Flows (Same Page)

- [Create new chatbot](create-new-chatbot.md)
- [Open chatbot](open-chatbot.md)
- [Archive chatbot](archive-chatbot.md)
- [Delete chatbot](delete-chatbot.md)
- [Switch card/list view](switch-card-list-view.md)
- [Filter by status](filter-by-status.md)

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

### Step 2: Interact with button: user profile dropdown (Settings, Log out)

Use the **button: user profile dropdown (Settings, Log out)** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Log out" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /platform → [Log out]
```

## Related Pages

- **Landing Page** (`/`) — Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and
- **Login Page** (`/auth/login`) — Email/password login with social auth (Apple, Google, Meta) and forgot password link
