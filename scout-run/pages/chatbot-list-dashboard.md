# Chatbot List (Dashboard)

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/platform` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Organization-scoped dashboard showing all chatbots. Displays chatbot cards with name, plan badge (Pro/Demo), API key prefix, creator email, last activity, conversation and message counts. Tabs filter by status: Active, Pending, Archive, Demo. Supports card and list view toggles.

## Who Uses This

Authenticated team members who want to select a chatbot to analyze or create a new one.

## Preconditions

- User is authenticated
- User belongs to at least one organization

## Page Context

Primary entry point after login. Organization is auto-created on first visit if the user has none. Sidebar provides org-level navigation: Chatbots, Members, Settings. User can switch organizations via the org switcher in the sidebar.

## Key Actions

- View chatbot list with status tabs
- Switch between card and list view
- Click a chatbot card to open its dashboard
- Click '+ New chatbot' to create a new chatbot
- Access Demo chatbots for exploration
- Navigate to Members or Settings via sidebar
- Switch organization via sidebar org switcher

## Expected Outcome

User selects a chatbot and navigates to its detailed dashboard, or creates a new chatbot.

## Interactive Elements

- button: New chatbot
- tabs: Active/Pending/Archive/Demo
- button: Card view
- button: List view
- link: chatbot cards
- sidebar: Chatbots/Members/Settings
- button: org switcher

## Flows Starting Here

- [Create new chatbot](../flows/create-new-chatbot.md) — Start the process of adding a new chatbot to the organization for analytics tracking.
- [Explore demo chatbot](../flows/explore-demo-chatbot.md) — Open a read-only demo chatbot to explore the full OpenBat dashboard without needing real data. Useful for evaluation and onboarding.

## Navigation Path

```
http://openbat.dev/auth/login → /platform
```
