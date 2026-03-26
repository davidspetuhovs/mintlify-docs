# Filter by date range

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter by date range |
| **Starting Page** | Chatbot Overview Dashboard |
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Change the date range for all dashboard analytics to focus on a specific time period.

## Who Uses This

Any dashboard user who wants to analyze data for a specific week, month, or custom range.

## Preconditions

- User is logged in
- On the chatbot dashboard

## Page Context

Main analytics dashboard for a specific chatbot. Shows stat cards (Conversations, Messages, Avg Sentiment, Analyzed Today), date range picker, segment filter (by Plan), and two tabs: User Insights and Assistant Performance. User Insights tab includes: sentiment trend chart, top user frustrations table, most dissatisfied users with investigate links, support topics table, revenue signals (churn risk, buying signals, capability gaps), top intents chart, sentiment by segment, activity heatmap, and languages breakdown. Assistant Performance tab includes: behavior alerts table (Hallucinating, Dodging, Verbose, Redirecting with severity), resolution outcomes donut chart, quality flags table, and capability gaps table.

## Steps

### Step 1

Navigate to /platform/[chatbotId]

{{screenshot_1}}

### Step 2

Click the date range button (shows 'This month' by default)

{{screenshot_2}}

### Step 3

Select a predefined range or pick custom dates

{{screenshot_3}}

### Step 4

Dashboard data refreshes for the selected period

{{screenshot_4}}

## Expected Outcome

All dashboard widgets update to show data for the selected date range.

## What Can Go Wrong

- No data available for the selected period

## Related Flows

- [View user insights](view-user-insights.md)
- [View assistant performance](view-assistant-performance.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId] → [Filter by date range]
```
