# Investigate dissatisfied user

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Investigate dissatisfied user |
| **Starting Page** | Chatbot Overview Dashboard |
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Click through from the 'Most dissatisfied users' section to view all conversations for a specific unhappy user, filtered by their email.

## Who Uses This

Customer success manager who wants to understand why a specific user is dissatisfied and take action.

## Preconditions

- User is logged in
- Dashboard shows dissatisfied users with analyzed sentiment

## Page Context

Main analytics dashboard for a specific chatbot. Shows stat cards (Conversations, Messages, Avg Sentiment, Analyzed Today), date range picker, segment filter (by Plan), and two tabs: User Insights and Assistant Performance. User Insights tab includes: sentiment trend chart, top user frustrations table, most dissatisfied users with investigate links, support topics table, revenue signals (churn risk, buying signals, capability gaps), top intents chart, sentiment by segment, activity heatmap, and languages breakdown. Assistant Performance tab includes: behavior alerts table (Hallucinating, Dodging, Verbose, Redirecting with severity), resolution outcomes donut chart, quality flags table, and capability gaps table.

## Steps

### Step 1

Navigate to /platform/[chatbotId]

{{screenshot_1}}

### Step 2

Scroll to 'Most dissatisfied users' section in User Insights tab

{{screenshot_2}}

### Step 3

Click the 'Investigate →' link next to the user's name

{{screenshot_3}}

### Step 4

User is navigated to the conversations page filtered by that user's email

{{screenshot_4}}

## Expected Outcome

Conversations page shows only conversations from the selected user, allowing the team to review their interactions.

## What Can Go Wrong

- No conversations found for the user in the selected date range

## Related Flows

- [View conversation detail](view-conversation-detail.md)
- [View user insights](view-user-insights.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId] → [Investigate dissatisfied user]
```
