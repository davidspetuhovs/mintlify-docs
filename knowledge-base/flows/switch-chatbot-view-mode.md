# Switch chatbot view mode

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Switch chatbot view mode |
| **Starting Page** | Platform Dashboard — Chatbot List |
| **URL** | `/platform` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Toggle between card view (visual cards with stats) and list view (compact table) for the chatbot list.

## Who Uses This

User with many chatbots who prefers a denser layout.

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

Click the 'List view' or 'Card view' toggle button in the top right area

{{screenshot_2}}

## Expected Outcome

The chatbot list switches between card grid and table list layouts.

## Related Flows

- [Filter chatbots by status](filter-chatbots-by-status.md)

## Navigation Path

```
http://localhost:3000 → /platform → [Switch chatbot view mode]
```
