# Sign In

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/auth/login` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Email/password authentication page for returning users. Minimal dark-themed form with OpenBat branding, email field, password field, forgot password link, and sign-up link.

## Who Uses This

Returning users who already have an OpenBat account and want to access their dashboard.

## Preconditions

- User has an existing OpenBat account
- User is not already logged in

## Page Context

Accessed from the landing page 'Sign in' button, or by direct navigation. Redirects to /platform on successful login. Part of the auth flow alongside sign-up and forgot-password.

## Key Actions

- Enter email address
- Enter password
- Click Sign in
- Navigate to forgot password
- Navigate to create account

## Expected Outcome

User authenticates and is redirected to the platform dashboard.

## Interactive Elements

- textbox: Email
- textbox: Password
- button: Sign in
- link: Forgot?
- link: Create an account

## Flows Starting Here

- [Email login](../flows/email-login.md) — Authenticate using email and password credentials to access the main dashboard. Primary authentication method for existing users.

## Navigation Path

```
http://openbat.dev/auth/login → /auth/login
```
