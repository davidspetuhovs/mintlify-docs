# View user insights

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View user insights |
| **Starting Page** | Chatbot Overview Dashboard |
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Review the User Insights tab to understand customer sentiment trends, frustration patterns, support topics, revenue signals, and user behavior over time.

## Who Uses This

Product manager or CS lead wanting to understand how users feel about their chatbot and identify actionable patterns.

## Preconditions

- User is logged in
- Chatbot has received conversations with analyzed messages

## Page Context

Main analytics dashboard for a specific chatbot. Shows stat cards (Conversations, Messages, Avg Sentiment, Analyzed Today), date range picker, segment filter (by Plan), and two tabs: User Insights and Assistant Performance. User Insights tab includes: sentiment trend chart, top user frustrations table, most dissatisfied users with investigate links, support topics table, revenue signals (churn risk, buying signals, capability gaps), top intents chart, sentiment by segment, activity heatmap, and languages breakdown. Assistant Performance tab includes: behavior alerts table (Hallucinating, Dodging, Verbose, Redirecting with severity), resolution outcomes donut chart, quality flags table, and capability gaps table.

## Steps

### Step 1

Navigate to /platform/[chatbotId]

{{screenshot_1}}

### Step 2

The User Insights tab is selected by default

{{screenshot_2}}

### Step 3

Review the sentiment trend chart to see satisfaction over time

{{screenshot_3}}

### Step 4

Check 'Top user frustrations' for recurring pain points

{{screenshot_4}}

### Step 5

Review 'Most dissatisfied users' and click 'Investigate' to see their conversations

{{screenshot_5}}

### Step 6

Scroll to 'Support topics' to see what users are talking about

{{screenshot_6}}

### Step 7

Check 'Revenue signals' for churn risk and buying signal indicators

{{screenshot_7}}

### Step 8

Review 'Top intents' to understand what users are asking about

{{screenshot_8}}

## Expected Outcome

User has a comprehensive view of customer sentiment and can identify areas needing attention.

## What Can Go Wrong

- No data available if no conversations have been analyzed yet

## Related Flows

- [View assistant performance](view-assistant-performance.md)
- [Investigate dissatisfied user](investigate-dissatisfied-user.md)
- [Filter by date range](filter-by-date-range.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId] → [View user insights]
```
