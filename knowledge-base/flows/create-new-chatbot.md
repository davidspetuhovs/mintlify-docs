# Create new chatbot

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Create new chatbot |
| **Starting Page** | Platform Dashboard — Chatbot List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Add a new chatbot to the organization to begin capturing and analyzing conversations from a new AI assistant deployment.

## Who Uses This

Product or engineering team member setting up OpenBat tracking for a new or existing AI chatbot.

## Preconditions

- User is logged in
- User has an organization

## Page Context

The main authenticated landing page showing all chatbots belonging to the user's organization. Displays chatbot cards with name, API key prefix, creator, creation date, conversation count, and message count. Supports filtering by status (Active, Pending, Archive) and switching between card and list views. Each chatbot card has a context menu (three-dot button) with Open chatbot, Archive, and Delete actions.

## Steps

### Step 1

Navigate to /platform

{{screenshot_1}}

### Step 2

Click the '+ New chatbot' button in the top right

{{screenshot_2}}

### Step 3

Fill in the chatbot creation form (name, etc.)

{{screenshot_3}}

### Step 4

Submit the form to create the chatbot

{{screenshot_4}}

### Step 5

Copy the generated API key

{{screenshot_5}}

### Step 6

Complete onboarding steps

{{screenshot_6}}

## Expected Outcome

A new chatbot is created with an API key. User is directed to the onboarding page to set up the SDK.

## What Can Go Wrong

- Chatbot name already exists
- Plan limit on number of chatbots reached

## Related Flows

- [Chatbot onboarding](chatbot-onboarding.md)
- [View chatbot dashboard](view-chatbot-dashboard.md)

## Navigation Path

```
http://localhost:3000 → /platform → [Create new chatbot]
```
