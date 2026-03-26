# Review conversation analysis

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Review conversation analysis |
| **Starting Page** | Conversation Detail |
| **URL** | `/platform/[chatbotId]/conversations/[conversationId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Read through a full conversation and examine the AI-generated analysis badges on each message to understand user sentiment, assistant behavior, and conversation outcomes.

## Who Uses This

CS manager or prompt engineer investigating a specific conversation flagged by the system or reviewing a dissatisfied user's interaction.

## Preconditions

- User is logged in
- Conversation exists and has been analyzed

## Page Context

Detailed view of a single conversation showing a chat-bubble interface with user and assistant messages in chronological order. Each message has timestamp, and analyzed messages show behavior/intent/sentiment badges (e.g., 'Dodging', 'Deflected', 'Helpful', 'conversational greeting'). Highlighted text spans within messages indicate detected patterns. Right sidebar shows: Overall Sentiment card, Conversation metadata (Messages, Conv ID, First/Last message, Created), User info (Name, Email, User ID), Organization info (Name, Org ID), Session info (Referrer, Device), Custom Metadata. Breadcrumb navigation back to conversations list. Filter and View buttons available.

## Steps

### Step 1

Navigate to the conversation detail page from the conversations list or an 'Investigate' link

{{screenshot_1}}

### Step 2

Read through user and assistant messages in the chat bubble view

{{screenshot_2}}

### Step 3

Review colored badges on messages: behavior tags (Dodging, Helpful), resolution tags (Deflected, Partially Resolved), intent tags

{{screenshot_3}}

### Step 4

Click on highlighted text spans to see details of detected patterns

{{screenshot_4}}

### Step 5

Check the right sidebar for overall sentiment, conversation metadata, user info, and organization context

{{screenshot_5}}

### Step 6

Use breadcrumb to navigate back to the conversations list

{{screenshot_6}}

## Expected Outcome

User has a complete understanding of the conversation including what the user asked, how the bot responded, and what the AI analysis detected.

## What Can Go Wrong

- Analysis not yet complete (badges won't appear)
- No sentiment data if analysis is disabled

## Related Flows

- [Browse conversations](browse-conversations.md)
- [Investigate dissatisfied user](investigate-dissatisfied-user.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/conversations/[conversationId] → [Review conversation analysis]
```
