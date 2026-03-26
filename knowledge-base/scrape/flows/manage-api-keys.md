# Manage API keys

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Manage API keys |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Chatbot configuration with 6 tabs: General, Company Info, API Keys, Members, Webhooks, Import/Export Data

### Starting Page Screenshot

![Chatbot Settings](../screenshots/page-16.png)

## Business Purpose

This flow allows users to **manage api keys** from the Chatbot Settings page.

## Related Flows (Same Page)

- [Rename chatbot](rename-chatbot.md)
- [Manage members](manage-members.md)
- [Configure webhooks](configure-webhooks.md)
- [Import/Export data](import-export-data.md)

## Available UI Elements

The following interactive elements are available on this page:

- tab: General
- tab: Company Info
- tab: API Keys
- tab: Members
- tab: Webhooks
- tab: Import/Export Data
- textbox: Chatbot name
- button: Save
- button: Copy Chatbot ID

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/settings` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with tab: API Keys

Use the **tab: API Keys** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Manage API keys" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Manage API keys]
```

## Related Pages

- **Analysis Config** (`/platform/[chatbotId]/analysis-config`) — Configuration for conversation analysis with 5 tabs: Metadata, Translation, User Analysis, Assistant
