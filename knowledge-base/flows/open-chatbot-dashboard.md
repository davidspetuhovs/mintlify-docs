# Open chatbot dashboard

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Open chatbot dashboard |
| **Starting Page** | Platform Dashboard — Chatbot List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Navigate into a specific chatbot's analytics dashboard to view conversation data, sentiment trends, and insights.

## Who Uses This

Team member who wants to review the analytics and health of a specific chatbot.

## Preconditions

- User is logged in
- At least one chatbot exists in the organization

## Page Context

The main authenticated landing page showing all chatbots belonging to the user's organization. Displays chatbot cards with name, API key prefix, creator, creation date, conversation count, and message count. Supports filtering by status (Active, Pending, Archive) and switching between card and list views. Each chatbot card has a context menu (three-dot button) with Open chatbot, Archive, and Delete actions.

## Steps

### Step 1

Navigate to /platform

{{screenshot_1}}

### Step 2

Click on a chatbot card to navigate to its dashboard

{{screenshot_2}}

### Step 3

Alternatively, click the three-dot menu and select 'Open chatbot'

{{screenshot_3}}

## Expected Outcome

User is navigated to /platform/[chatbotId] showing the chatbot's overview dashboard with stats, sentiment charts, and insights.

## What Can Go Wrong

- Chatbot may redirect to onboarding if not yet set up

## Related Flows

- [View chatbot dashboard](view-chatbot-dashboard.md)
- [Chatbot onboarding](chatbot-onboarding.md)

## Navigation Path

```
http://localhost:3000 → /platform → [Open chatbot dashboard]
```
