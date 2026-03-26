# Navigate to forgot password

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Navigate to forgot password |
| **Starting Page** | Login Page |
| **URL** | `/auth/login` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Start the password reset process when a user has forgotten their credentials.

## Who Uses This

User who cannot remember their password and needs to reset it.

## Preconditions

- User has an existing account
- User knows their email but forgot their password

## Page Context

Authentication page where existing users log in to their OpenBat account. Features a split layout with a login form on the left and a decorative image on the right. Supports email/password login and social authentication via Apple, Google, and Meta. Includes a link to the forgot password flow.

## Steps

### Step 1

Navigate to /auth/login

{{screenshot_1}}

### Step 2

Click the 'Forgot your password?' link next to the Password field

{{screenshot_2}}

### Step 3

User is redirected to /auth/forgot-password

{{screenshot_3}}

## Expected Outcome

User lands on the password reset page with an email input field.

## Related Flows

- [Forgot password flow](forgot-password-flow.md)
- [Email login](email-login.md)

## Navigation Path

```
http://localhost:3000 → /auth/login → [Navigate to forgot password]
```
