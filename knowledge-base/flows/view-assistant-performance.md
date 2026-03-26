# View assistant performance

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View assistant performance |
| **Starting Page** | Chatbot Overview Dashboard |
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Review the Assistant Performance tab to identify problematic bot behaviors, resolution rates, quality issues, and capability gaps.

## Who Uses This

Engineering lead or bot prompt engineer who wants to improve chatbot response quality.

## Preconditions

- User is logged in
- Chatbot has analyzed assistant messages

## Page Context

Main analytics dashboard for a specific chatbot. Shows stat cards (Conversations, Messages, Avg Sentiment, Analyzed Today), date range picker, segment filter (by Plan), and two tabs: User Insights and Assistant Performance. User Insights tab includes: sentiment trend chart, top user frustrations table, most dissatisfied users with investigate links, support topics table, revenue signals (churn risk, buying signals, capability gaps), top intents chart, sentiment by segment, activity heatmap, and languages breakdown. Assistant Performance tab includes: behavior alerts table (Hallucinating, Dodging, Verbose, Redirecting with severity), resolution outcomes donut chart, quality flags table, and capability gaps table.

## Steps

### Step 1

Navigate to /platform/[chatbotId]

{{screenshot_1}}

### Step 2

Click the 'Assistant Performance' tab

{{screenshot_2}}

### Step 3

Review 'Behavior alerts' for problematic behaviors (hallucinating, dodging, verbose, redirecting) with severity levels

{{screenshot_3}}

### Step 4

Check the 'Resolution outcomes' donut chart for resolution rates

{{screenshot_4}}

### Step 5

Review 'Quality flags' for issues like hallucination risk and sensitive data exposure

{{screenshot_5}}

### Step 6

Check 'Capability gaps' for unmet feature requests

{{screenshot_6}}

## Expected Outcome

User understands bot behavior patterns and can prioritize prompt improvements.

## What Can Go Wrong

- No assistant analysis data if assistant message analysis is disabled in settings

## Related Flows

- [View user insights](view-user-insights.md)
- [Configure analysis settings](configure-analysis-settings.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId] → [View assistant performance]
```
