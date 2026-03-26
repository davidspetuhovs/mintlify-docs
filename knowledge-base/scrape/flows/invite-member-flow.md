# Invite member flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Invite member flow |
| **Starting Page** | Organization Members |
| **URL** | `/platform/members` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Team member management with email, role, and join date

## Business Purpose

This flow allows users to **invite member flow** from the Organization Members page.

## Available UI Elements

The following interactive elements are available on this page:

- table: Email/Role/Joined
- button: Invite member

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/members` and verify the page loads correctly.

### Step 2: Interact with button: Invite member

Use the **button: Invite member** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Invite member flow" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /platform/members → [Invite member flow]
```
