# Invite team member

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Invite team member |
| **Starting Page** | Organization Members |
| **URL** | `/platform/members` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Add a new member to the organization so they can access chatbot dashboards and analytics alongside the team.

## Who Uses This

Organization owner or admin who wants to give a colleague access to OpenBat.

## Preconditions

- User is logged in
- User has appropriate permissions (Owner role)

## Page Context

Manage team members who have access to the organization. Displays a table of members with their email, role (Owner, etc.), and join date. Includes an 'Invite member' button to add new team members.

## Steps

### Step 1

Navigate to /platform/members

{{screenshot_1}}

### Step 2

Click the '+ Invite member' button

{{screenshot_2}}

### Step 3

Enter the new member's email address in the invitation form

{{screenshot_3}}

### Step 4

Select a role for the new member

{{screenshot_4}}

### Step 5

Submit the invitation

{{screenshot_5}}

## Expected Outcome

An invitation is sent to the provided email. The member appears in the table once they accept.

## What Can Go Wrong

- Email already a member
- Plan limit on team members reached
- Invalid email format

## Navigation Path

```
http://localhost:3000 → /platform/members → [Invite team member]
```
