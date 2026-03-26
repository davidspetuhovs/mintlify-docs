# Browse client organizations

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Browse client organizations |
| **Starting Page** | Client Organizations |
| **URL** | `/platform/[chatbotId]/organizations` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

View all customer organizations that have used the chatbot, sorted and filtered to understand which organizations are most active, most dissatisfied, or generate the most conversations.

## Who Uses This

Customer success manager wanting to identify high-risk or high-value client organizations.

## Preconditions

- User is logged in
- Chatbot has captured conversations with organization metadata

## Page Context

Paginated table of customer organizations that have interacted with the chatbot. Columns: Organization, Plan (demo/client), Industry, MRR, Conversations, Users, Sentiment (with colored badge), Last Activity. Supports text search, filtering, view configuration, column sorting, and date range selection. 48 rows with pagination.

## Steps

### Step 1

Navigate to /platform/[chatbotId]/organizations

{{screenshot_1}}

### Step 2

Browse the organizations table

{{screenshot_2}}

### Step 3

Sort by Sentiment to find the most dissatisfied organizations

{{screenshot_3}}

### Step 4

Sort by Conversations or Users to find the most active organizations

{{screenshot_4}}

### Step 5

Use the search box to find a specific organization

{{screenshot_5}}

### Step 6

Click on an organization row to see its details

{{screenshot_6}}

## Expected Outcome

User can identify which client organizations need attention based on sentiment, activity, and engagement data.

## What Can Go Wrong

- No organization data if conversations don't include organization metadata

## Related Flows

- [Browse conversations](browse-conversations.md)
- [Browse chatbot users](browse-chatbot-users.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/organizations → [Browse client organizations]
```
