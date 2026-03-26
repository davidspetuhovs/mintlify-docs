# Rename organization

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Rename organization |
| **Starting Page** | Organization Settings |
| **URL** | `/platform/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Organization name editing and danger zone with delete option

## Business Purpose

This flow allows users to **rename organization** from the Organization Settings page.

## Related Flows (Same Page)

- [Delete organization](delete-organization.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Organization name
- button: Save
- button: Delete organization

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/settings` and verify the page loads correctly.

### Step 2: Interact with textbox: Organization name

Use the **textbox: Organization name** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Delete organization

Use the **button: Delete organization** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Rename organization" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /platform/settings → [Rename organization]
```

## Related Pages

- **Chatbot Settings** (`/platform/[chatbotId]/settings`) — Chatbot configuration with 6 tabs: General, Company Info, API Keys, Members, Webhooks, Import/Export
