# Delete chatbot

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Delete chatbot |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Permanently delete a chatbot and all its associated conversations, messages, and analytics data. This is irreversible.

## Who Uses This

Admin who needs to remove a test or decommissioned chatbot.

## Preconditions

- User is logged in
- User has appropriate permissions

## Page Context

Comprehensive chatbot configuration page with six tabs: General (chatbot name, ID, creation date, message analysis toggles, delete chatbot), Company Info, API Keys, Members, Webhooks, Import/Export Data. The General tab includes toggles for enabling/disabling user and assistant message analysis, and a danger zone for permanently deleting the chatbot.

### Starting Page

![Chatbot Settings](../screenshots/page-16.png)

## Steps

### Step 1

Navigate to /platform/[chatbotId]/settings

{{screenshot_1}}

### Step 2

Scroll to the 'Danger zone' section at the bottom

{{screenshot_2}}

### Step 3

Click the 'Delete chatbot' button

{{screenshot_3}}

### Step 4

Confirm the deletion in the confirmation dialog

{{screenshot_4}}

## Expected Outcome

The chatbot and all its data are permanently deleted. User is redirected to the chatbot list at /platform.

## What Can Go Wrong

- User cancels the confirmation
- Insufficient permissions

## Related Flows

- [Create new chatbot](create-new-chatbot.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Delete chatbot]
```
