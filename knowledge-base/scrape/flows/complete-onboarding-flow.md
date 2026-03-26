# Complete onboarding flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Complete onboarding flow |
| **Starting Page** | Chatbot Onboarding |
| **URL** | `/platform/[chatbotId]/onboarding` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

SDK setup instructions for new chatbots. Redirects to dashboard if already onboarded

### Starting Page Screenshot

![Chatbot Onboarding](../screenshots/page-17.png)

## Business Purpose

This flow allows users to **complete onboarding flow** from the Chatbot Onboarding page.

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/onboarding` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Verify outcome

Verify that the "Complete onboarding flow" completed successfully and the expected state change occurred.

{{screenshot_2}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/onboarding → [Complete onboarding flow]
```
