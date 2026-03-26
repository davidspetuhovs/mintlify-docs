# View conversation messages

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View conversation messages |
| **Starting Page** | Conversation Detail |
| **URL** | `/platform/[chatbotId]/conversations/[id]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Chat bubble view of a conversation with right sidebar showing overall sentiment, conversation metadata, and user info

### Starting Page Screenshot

![Conversation Detail](../screenshots/page-11.png)

## Business Purpose

This flow allows users to **view conversation messages** from the Conversation Detail page.

## Related Flows (Same Page)

- [Navigate back to conversations](navigate-back-to-conversations.md)

## Available UI Elements

The following interactive elements are available on this page:

- breadcrumb: Conversations > User
- button: Filter
- button: View
- section: Overall Sentiment
- section: Conversation metadata (messages, conv ID, timestamps)
- section: User info

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/conversations/[id]` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with breadcrumb: Conversations > User

Use the **breadcrumb: Conversations > User** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: View

Use the **button: View** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with section: Conversation metadata (messages, conv ID, timestamps)

Use the **section: Conversation metadata (messages, conv ID, timestamps)** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "View conversation messages" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/conversations/[id] → [View conversation messages]
```

## Related Pages

- **Landing Page** (`/`) — Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and
- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Chatbot Dashboard** (`/platform/[chatbotId]`) — Overview dashboard with stats (conversations, messages, avg sentiment, analyzed today), date range s
