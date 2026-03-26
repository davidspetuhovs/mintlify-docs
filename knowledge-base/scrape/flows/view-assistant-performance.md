# View assistant performance

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View assistant performance |
| **Starting Page** | Chatbot Dashboard |
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Overview dashboard with stats (conversations, messages, avg sentiment, analyzed today), date range selector, segment filter, and two tabs: User Insights and Assistant Performance

## Business Purpose

This flow allows users to **view assistant performance** from the Chatbot Dashboard page.

## Related Flows (Same Page)

- [View user insights](view-user-insights.md)
- [Change date range](change-date-range.md)
- [Segment by plan](segment-by-plan.md)
- [Investigate dissatisfied user](investigate-dissatisfied-user.md)

## Available UI Elements

The following interactive elements are available on this page:

- button: date range selector
- combobox: Segment by Plan
- tab: User Insights
- tab: Assistant Performance
- chart: User sentiment trend
- table: Top user frustrations
- table: Most dissatisfied users
- table: Support topics
- section: Revenue signals
- chart: Top intents
- section: Sentiment by segment
- chart: Activity heatmap
- section: Languages
- section: Behavior alerts (Assistant Performance)
- chart: Resolution outcomes (Assistant Performance)

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]` and verify the page loads correctly.

### Step 2: Interact with tab: Assistant Performance

Use the **tab: Assistant Performance** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with section: Behavior alerts (Assistant Performance)

Use the **section: Behavior alerts (Assistant Performance)** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with chart: Resolution outcomes (Assistant Performance)

Use the **chart: Resolution outcomes (Assistant Performance)** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "View assistant performance" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId] → [View assistant performance]
```

## Related Pages

- **Landing Page** (`/`) — Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and
- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Conversation Detail** (`/platform/[chatbotId]/conversations/[id]`) — Chat bubble view of a conversation with right sidebar showing overall sentiment, conversation metada
