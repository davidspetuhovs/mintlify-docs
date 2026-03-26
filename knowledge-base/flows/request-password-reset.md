# Request password reset

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Request password reset |
| **Starting Page** | Forgot Password Page |
| **URL** | `/auth/forgot-password` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Submit an email address to receive a password reset link, allowing the user to regain access to their account.

## Who Uses This

Existing user who forgot their password and needs to reset it.

## Preconditions

- User has an existing account
- User knows their email address

## Page Context

Password reset page where users enter their email to receive a reset link. Simple form with email input and submit button.

## Steps

### Step 1

Navigate to /auth/forgot-password (or click 'Forgot your password?' from the login page)

{{screenshot_1}}

### Step 2

Enter the account email address in the Email field

{{screenshot_2}}

### Step 3

Click 'Send reset email'

{{screenshot_3}}

### Step 4

Check email inbox for the reset link

{{screenshot_4}}

## Expected Outcome

A password reset email is sent to the provided address with a link to set a new password.

## What Can Go Wrong

- Email not found in the system
- Email delivery failure
- Reset link expired

## Related Flows

- [Email login](email-login.md)

## Navigation Path

```
http://localhost:3000 → /auth/forgot-password → [Request password reset]
```
