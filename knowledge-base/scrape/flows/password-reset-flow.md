# Password reset flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Password reset flow |
| **Starting Page** | Forgot Password Page |
| **URL** | `/auth/forgot-password` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Password reset form with email input

## Business Purpose

This flow allows users to **password reset flow** from the Forgot Password Page page.

## Available UI Elements

The following interactive elements are available on this page:

- textbox: Email
- button: Send reset email
- link: Login

## Steps

### Step 1: Navigate to starting page

Navigate to `/auth/forgot-password` and verify the page loads correctly.

### Step 2: Interact with button: Send reset email

Use the **button: Send reset email** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Password reset flow" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → /auth/forgot-password → [Password reset flow]
```

## Related Pages

- **Login Page** (`/auth/login`) — Email/password login with social auth (Apple, Google, Meta) and forgot password link
