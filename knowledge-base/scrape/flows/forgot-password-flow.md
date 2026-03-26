# Forgot password flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Forgot password flow |
| **Starting Page** | Login Page |
| **URL** | `/auth/login` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Email/password login with social auth (Apple, Google, Meta) and forgot password link

## Business Purpose

This flow allows users to **forgot password flow** from the Login Page page.

## Related Flows (Same Page)

- [Email/password login](email-password-login.md)
- [Social auth login](social-auth-login.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Email
- textbox: Password
- button: Login
- button: Login with Apple
- button: Login with Google
- button: Login with Meta
- link: Forgot your password?
- link: Terms of Service
- link: Privacy Policy

## Steps

### Step 1: Navigate to starting page

Navigate to `/auth/login` and verify the page loads correctly.

### Step 2: Interact with textbox: Password

Use the **textbox: Password** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with link: Forgot your password?

Use the **link: Forgot your password?** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Forgot password flow" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /auth/login → [Forgot password flow]
```
