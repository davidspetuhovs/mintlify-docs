# Manage API keys

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Manage API keys |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

View, create, or rotate API keys used by the SDK to send conversation data to this chatbot.

## Who Uses This

Developer integrating the OpenBat SDK who needs to copy or rotate the API key.

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

Click the 'API Keys' tab

{{screenshot_2}}

### Step 3

View existing API key prefix

{{screenshot_3}}

### Step 4

Rotate the key if needed

{{screenshot_4}}

## Expected Outcome

API key is visible (prefix only) and can be rotated for security.

## What Can Go Wrong

- Rotating key invalidates the old key immediately

## Related Flows

- [Chatbot onboarding](chatbot-onboarding.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Manage API keys]
```
