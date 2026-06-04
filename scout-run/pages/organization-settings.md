# Organization Settings

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/platform/settings` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Organization-level settings with editable organization name and a danger zone for permanent organization deletion.

## Who Uses This

Organization owner managing the org configuration.

## Preconditions

- User is authenticated
- User is the organization owner

## Page Context

Accessed from the organization-level sidebar. Top-level settings for the organization (not chatbot-specific).

## Key Actions

- Edit organization display name
- Delete organization (destructive, requires confirmation)

## Expected Outcome

Organization settings are updated, or the organization is permanently deleted.

## Interactive Elements

- textbox: Organization name
- button: Save
- button: Delete organization (danger zone)

## Navigation Path

```
http://openbat.dev/auth/login → /platform/settings
```
