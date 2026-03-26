# Rename chatbot

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Rename chatbot |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Chatbot configuration with 6 tabs: General, Company Info, API Keys, Members, Webhooks, Import/Export Data

### Starting Page Screenshot

![Chatbot Settings](../screenshots/page-16.png)

## Business Purpose

This flow allows users to **rename chatbot** from the Chatbot Settings page.

## Related Flows (Same Page)

- [Manage API keys](manage-api-keys.md)
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

### Step 2: Interact with textbox: Chatbot name

Use the **textbox: Chatbot name** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Copy Chatbot ID

Use the **button: Copy Chatbot ID** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Rename chatbot" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Rename chatbot]
```

## Related Pages

- **Organization Settings** (`/platform/settings`) — Organization name editing and danger zone with delete option
