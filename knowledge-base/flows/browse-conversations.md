# Browse conversations

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Browse conversations |
| **Starting Page** | Conversations List |
| **URL** | `/platform/[chatbotId]/conversations` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Browse, search, and filter all captured chatbot conversations to find specific interactions or patterns.

## Who Uses This

Team member reviewing recent conversations to understand user behavior and chatbot performance.

## Preconditions

- User is logged in
- Chatbot has captured conversations

## Page Context

Paginated table of all conversations captured by this chatbot. Columns: User, Email, Organization, Messages, Sentiment (with colored badge and score), Language (flag), Plan, Last Message, Created. Supports text search, column sorting, filter button, view configuration, date range selection, and pagination (20 rows per page). Clicking a row navigates to the conversation detail page.

### Starting Page

![Conversations List](../screenshots/page-10.png)

## Steps

### Step 1

Navigate to /platform/[chatbotId]/conversations

{{screenshot_1}}

### Step 2

Browse the conversation table sorted by most recent

{{screenshot_2}}

### Step 3

Optionally type in the search box to filter by user name, email, or organization

{{screenshot_3}}

### Step 4

Click column headers to sort by Messages, Sentiment, Last Message, etc.

{{screenshot_4}}

### Step 5

Use pagination controls to browse through pages

{{screenshot_5}}

### Step 6

Click on a conversation row to view its detail

{{screenshot_6}}

## Expected Outcome

User can find and navigate to specific conversations for detailed review.

## What Can Go Wrong

- No conversations exist yet
- Search returns no results

## Related Flows

- [View conversation detail](view-conversation-detail.md)
- [Filter by date range](filter-by-date-range.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/conversations → [Browse conversations]
```
