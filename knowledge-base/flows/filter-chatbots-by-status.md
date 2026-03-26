# Filter chatbots by status

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Filter chatbots by status |
| **Starting Page** | Platform Dashboard — Chatbot List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Filter the chatbot list to show only Active, Pending, or Archived chatbots.

## Who Uses This

User managing multiple chatbots who wants to focus on a specific group.

## Preconditions

- User is logged in
- On the /platform page

## Page Context

The main authenticated landing page showing all chatbots belonging to the user's organization. Displays chatbot cards with name, API key prefix, creator, creation date, conversation count, and message count. Supports filtering by status (Active, Pending, Archive) and switching between card and list views. Each chatbot card has a context menu (three-dot button) with Open chatbot, Archive, and Delete actions.

## Steps

### Step 1

Navigate to /platform

{{screenshot_1}}

### Step 2

Click one of the status filter buttons: Active, Pending, or Archive

{{screenshot_2}}

## Expected Outcome

The chatbot list filters to show only chatbots matching the selected status.

## Related Flows

- [Open chatbot dashboard](open-chatbot-dashboard.md)

## Navigation Path

```
http://localhost:3000 → /platform → [Filter chatbots by status]
```
