# Create Account

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/auth/sign-up` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Registration page for new users. Collects work email, password, and password confirmation. Sends a verification email on submit. Includes terms and privacy policy links.

## Who Uses This

New users who want to start using OpenBat for their chatbot analytics.

## Preconditions

- User does not have an existing account

## Page Context

Reached from the landing page CTA or the login page 'Create an account' link. After submission, redirects to /auth/sign-up-success.

## Key Actions

- Enter work email
- Enter password (min 8 chars)
- Confirm password
- Click Create account
- Read terms and privacy policy

## Expected Outcome

Account is created, verification email is sent, user sees confirmation page.

## Interactive Elements

- textbox: Work Email
- textbox: Password
- textbox: Confirm Password
- button: Create account
- link: Terms
- link: Privacy Policy

## Flows Starting Here

- [Email sign up](../flows/email-sign-up.md) — Create a new OpenBat account with email and password. A verification email is sent to confirm the address before the account becomes fully active.

## Navigation Path

```
http://openbat.dev/auth/login → /auth/sign-up
```
