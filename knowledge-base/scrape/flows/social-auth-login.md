# Social auth login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Social auth login |
| **Starting Page** | Login Page |
| **URL** | `/auth/login` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Email/password login with social auth (Apple, Google, Meta) and forgot password link

## Business Purpose

This flow allows users to **social auth login** from the Login Page page.

## Related Flows (Same Page)

- [Email/password login](email-password-login.md)
- [Forgot password flow](forgot-password-flow.md)

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

### Step 2: Interact with button: Login

Use the **button: Login** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: Login with Apple

Use the **button: Login with Apple** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with button: Login with Google

Use the **button: Login with Google** element to progress through the flow.

{{screenshot_4}}

### Step 5: Interact with button: Login with Meta

Use the **button: Login with Meta** element to progress through the flow.

{{screenshot_5}}

### Step 6: Verify outcome

Verify that the "Social auth login" completed successfully and the expected state change occurred.

{{screenshot_6}}

## Navigation Path

```
http://localhost:3000 → /auth/login → [Social auth login]
```

## Related Pages

- **Sign Up Page** (`/auth/sign-up`) — Account creation form with email, password, confirm password, social auth options
