# Organization Members

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/platform/members` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Team member management page showing a table of all organization members with email, role (Owner/Admin/Member), and join date. Supports inviting new members.

## Who Uses This

Organization owners or admins managing team access.

## Preconditions

- User is authenticated
- User has owner or admin role

## Page Context

Accessed from the organization-level sidebar. Sits alongside Chatbots and Settings in the org navigation.

## Key Actions

- View member list with roles
- Invite new member via email
- Manage member roles

## Expected Outcome

Team members are managed and new members can be invited to the organization.

## Interactive Elements

- table: Email/Role/Joined columns
- button: Invite member

## Flows Starting Here

- [Invite team member](../flows/invite-team-member.md) — Send an email invitation to add a new team member to the organization.

## Navigation Path

```
http://openbat.dev/auth/login → /platform/members
```
