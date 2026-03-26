# Social auth login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Social auth login |
| **Starting Page** | Login Page |
| **URL** | `/auth/login` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Authenticate using a third-party identity provider (Apple, Google, or Meta) for passwordless login.

## Who Uses This

User who prefers OAuth-based login over managing a separate password.

## Preconditions

- User has an account linked to the chosen social provider
- User is not already logged in

## Page Context

Authentication page where existing users log in to their OpenBat account. Features a split layout with a login form on the left and a decorative image on the right. Supports email/password login and social authentication via Apple, Google, and Meta. Includes a link to the forgot password flow.

## Steps

### Step 1

Navigate to /auth/login

{{screenshot_1}}

### Step 2

Click one of the social auth buttons (Apple, Google, or Meta)

{{screenshot_2}}

### Step 3

Complete the OAuth flow in the provider's popup/redirect

{{screenshot_3}}

### Step 4

Wait for authentication to complete and redirect to the dashboard

{{screenshot_4}}

## Expected Outcome

User is redirected to /platform showing their organization's chatbot list.

## What Can Go Wrong

- Social provider OAuth popup may be blocked
- Account not linked to chosen provider
- Network errors during OAuth flow

## Related Flows

- [Email login](email-login.md)
- [Email sign up](email-sign-up.md)

## Navigation Path

```
http://localhost:3000 → /auth/login → [Social auth login]
```
