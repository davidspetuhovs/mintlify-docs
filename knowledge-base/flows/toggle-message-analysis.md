# Toggle message analysis

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Toggle message analysis |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Enable or disable automatic analysis for user messages and/or assistant messages to control which signals are extracted.

## Who Uses This

Developer or admin who wants to disable assistant analysis to reduce costs or focus only on user sentiment.

## Preconditions

- User is logged in

## Page Context

Comprehensive chatbot configuration page with six tabs: General (chatbot name, ID, creation date, message analysis toggles, delete chatbot), Company Info, API Keys, Members, Webhooks, Import/Export Data. The General tab includes toggles for enabling/disabling user and assistant message analysis, and a danger zone for permanently deleting the chatbot.

### Starting Page

![Chatbot Settings](../screenshots/page-16.png)

## Steps

### Step 1

Navigate to /platform/[chatbotId]/settings

{{screenshot_1}}

### Step 2

Scroll to the 'Message analysis' section

{{screenshot_2}}

### Step 3

Toggle the 'User message analysis' switch to enable/disable user analysis (sentiment, intent, topics, flags)

{{screenshot_3}}

### Step 4

Toggle the 'Assistant message analysis' switch to enable/disable assistant analysis (behavior, outcome, quality, flags)

{{screenshot_4}}

## Expected Outcome

Future messages are analyzed (or not) according to the toggle settings.

## Related Flows

- [View user insights](view-user-insights.md)
- [View assistant performance](view-assistant-performance.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Toggle message analysis]
```
