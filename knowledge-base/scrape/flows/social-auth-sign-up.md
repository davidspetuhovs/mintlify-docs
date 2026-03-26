# Social auth sign up

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Social auth sign up |
| **Starting Page** | Sign Up Page |
| **URL** | `/auth/sign-up` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Account creation form with email, password, confirm password, social auth options

## Business Purpose

This flow allows users to **social auth sign up** from the Sign Up Page page.

## Related Flows (Same Page)

- [Email sign up](email-sign-up.md)

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Email
- textbox: Password
- textbox: Confirm Password
- button: Create Account
- button: Login with Apple
- button: Login with Google
- button: Login with Meta
- link: Sign in

## Steps

### Step 1: Navigate to starting page

Navigate to `/auth/sign-up` and verify the page loads correctly.

### Step 2: Interact with link: Sign in

Use the **link: Sign in** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Social auth sign up" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /auth/sign-up → [Social auth sign up]
```

## Related Pages

- **Login Page** (`/auth/login`) — Email/password login with social auth (Apple, Google, Meta) and forgot password link
