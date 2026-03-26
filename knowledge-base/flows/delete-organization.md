# Delete organization

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Delete organization |
| **Starting Page** | Organization Settings |
| **URL** | `/platform/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Permanently delete the organization and all associated chatbots, conversations, messages, and analytics data. This is an irreversible destructive action.

## Who Uses This

Organization owner who wants to completely remove their OpenBat account and all data.

## Preconditions

- User is logged in
- User is organization owner

## Page Context

Manage organization-level settings including the organization display name and a danger zone for permanently deleting the organization and all its data.

## Steps

### Step 1

Navigate to /platform/settings

{{screenshot_1}}

### Step 2

Scroll to the 'Danger zone' section

{{screenshot_2}}

### Step 3

Click the 'Delete organization' button

{{screenshot_3}}

### Step 4

Confirm the deletion in the confirmation dialog

{{screenshot_4}}

## Expected Outcome

The organization, all chatbots, conversations, messages, and analytics are permanently deleted. User is redirected to a logged-out or empty state.

## What Can Go Wrong

- User cancels the confirmation dialog
- Insufficient permissions

## Navigation Path

```
http://localhost:3000 → /platform/settings → [Delete organization]
```
