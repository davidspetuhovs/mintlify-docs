# Navigate to login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Navigate to login |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Access the authentication page to log in to an existing OpenBat account from the public landing page.

## Who Uses This

Returning user who already has an OpenBat account and wants to access their chatbot analytics dashboard.

## Preconditions

- User is not already logged in
- User has an existing account

## Page Context

Public marketing landing page for OpenBat — 'Google Analytics for AI chatbots'. Features hero section with value proposition, animated chat widget demo, logo carousel of supported AI providers, feature sections (conversation analysis, sentiment scoring, topic detection, workflow automation, SDK integration), pricing tiers (Free through Enterprise), FAQ accordion, testimonials, and CTA sections.

## Steps

### Step 1

Navigate to the landing page at /

{{screenshot_1}}

### Step 2

Click the 'Login' link in the top-right navigation header

{{screenshot_2}}

### Step 3

User is redirected to /auth/login

{{screenshot_3}}

## Expected Outcome

User lands on the login page with email/password form and social auth options.

## What Can Go Wrong

- Page may not load if server is down

## Related Flows

- [Email login](email-login.md)
- [Email sign up](email-sign-up.md)
- [Social auth login](social-auth-login.md)

## Navigation Path

```
http://localhost:3000 → / → [Navigate to login]
```
