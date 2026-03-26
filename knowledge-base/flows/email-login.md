# Email login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Email login |
| **Starting Page** | Login Page |
| **URL** | `/auth/login` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Authenticate using email and password credentials to access the main dashboard. This is the primary authentication method for existing users.

## Who Uses This

Returning user who already has an account and wants to access their chatbot analytics dashboard.

## Preconditions

- User has an existing account
- User is not already logged in
- User knows their email and password

## Page Context

Authentication page where existing users log in to their OpenBat account. Features a split layout with a login form on the left and a decorative image on the right. Supports email/password login and social authentication via Apple, Google, and Meta. Includes a link to the forgot password flow.

## Steps

### Step 1

Navigate to /auth/login

{{screenshot_1}}

### Step 2

Enter email address in the Email text field

{{screenshot_2}}

### Step 3

Enter password in the Password text field

{{screenshot_3}}

### Step 4

Click the 'Login' button to submit credentials

{{screenshot_4}}

### Step 5

Wait for authentication to complete and redirect to the dashboard

{{screenshot_5}}

## Expected Outcome

User is redirected to /platform showing their organization's chatbot list.

## What Can Go Wrong

- Invalid email or password shows an error
- Account may not exist yet

## Related Flows

- [Forgot password flow](forgot-password-flow.md)
- [Social auth login](social-auth-login.md)
- [Email sign up](email-sign-up.md)

## Navigation Path

```
http://localhost:3000 → /auth/login → [Email login]
```
