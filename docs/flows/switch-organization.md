# Switch organization

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Switch organization |
| **Starting Page** | `/platform` |
| **Persona** | User who manages multiple teams or products |

## Description

Switch between organizations using the sidebar switcher

## Preconditions

- User is logged in
- User belongs to multiple organizations

## Steps

### Step 1

Click organization switcher in sidebar

### Step 2

View dropdown with organizations list and 'Create organization' option

## Expected Outcome

Dashboard updates to show chatbots for the selected organization

## Failure Modes

### User only has one organization

Dropdown shows only current org and 'Create organization' option — no switching possible

## Related Flows

- [Rename organization](rename-organization.md)

## Alternative Paths

- Create a new organization from the switcher
