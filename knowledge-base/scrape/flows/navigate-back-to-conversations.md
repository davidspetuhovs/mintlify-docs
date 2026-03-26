# Navigate back to conversations

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Navigate back to conversations |
| **Starting Page** | Conversation Detail |
| **URL** | `/platform/[chatbotId]/conversations/[id]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Chat bubble view of a conversation with right sidebar showing overall sentiment, conversation metadata, and user info

### Starting Page Screenshot

![Conversation Detail](../screenshots/page-11.png)

## Business Purpose

This flow allows users to **navigate back to conversations** from the Conversation Detail page.

## Related Flows (Same Page)

- [View conversation messages](view-conversation-messages.md)

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

### Step 3: Verify outcome

Verify that the "Navigate back to conversations" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/conversations/[id] → [Navigate back to conversations]
```

## Related Pages

- **Conversations List** (`/platform/[chatbotId]/conversations`) — Paginated conversation table with sortable columns, search, filters, and date range. Supports filter
