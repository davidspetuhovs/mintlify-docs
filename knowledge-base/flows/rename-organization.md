# Rename organization

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Rename organization |
| **Starting Page** | Organization Settings |
| **URL** | `/platform/settings` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Change the display name of the organization that appears throughout the platform.

## Who Uses This

Organization owner who wants to update the organization name (e.g., after a company rebrand).

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

Clear the Organization name field and type the new name

{{screenshot_2}}

### Step 3

Click the 'Save' button

{{screenshot_3}}

## Expected Outcome

Organization name is updated and reflected across the platform UI.

## What Can Go Wrong

- Empty name not allowed
- Name too long

## Navigation Path

```
http://localhost:3000 → /platform/settings → [Rename organization]
```
