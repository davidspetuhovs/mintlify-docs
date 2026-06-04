# Forgot Password

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/auth/forgot-password` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Password reset request page. User enters their email to receive a one-time reset link. Links back to sign-in.

## Who Uses This

Existing user who has forgotten their password.

## Preconditions

- User has an existing account

## Page Context

Accessed from the login page 'Forgot?' link. After submission, a reset email is sent.

## Key Actions

- Enter email address
- Click Send reset link
- Navigate back to sign in

## Expected Outcome

Password reset email is sent with a one-time link to /auth/update-password.

## Interactive Elements

- textbox: Email
- button: Send reset link
- link: Back to sign in

## Flows Starting Here

- [Password reset request](../flows/password-reset-request.md) — Request a password reset email when the user has forgotten their credentials.

## Navigation Path

```
http://openbat.dev/auth/login → /auth/forgot-password
```
