# Rename chatbot

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Rename chatbot |
| **Starting Page** | Chatbot Settings |
| **URL** | `/platform/[chatbotId]/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Change the display name of a chatbot that appears throughout the dashboard.

## Who Uses This

Team member who wants to rename a chatbot for clarity (e.g., from 'test' to 'Production Support Bot').

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

The General tab is selected by default

{{screenshot_2}}

### Step 3

Clear the Chatbot name field and type the new name

{{screenshot_3}}

### Step 4

Click the 'Save' button

{{screenshot_4}}

## Expected Outcome

Chatbot name is updated and reflected throughout the dashboard.

## What Can Go Wrong

- Empty name not allowed

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/settings → [Rename chatbot]
```
