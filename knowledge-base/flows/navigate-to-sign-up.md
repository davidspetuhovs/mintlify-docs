# Navigate to sign up

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Navigate to sign up |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Start the account creation process from the landing page to begin using OpenBat for chatbot analytics.

## Who Uses This

New user who has learned about OpenBat and wants to create a free account.

## Preconditions

- User does not have an existing account

## Page Context

Public marketing landing page for OpenBat — 'Google Analytics for AI chatbots'. Features hero section with value proposition, animated chat widget demo, logo carousel of supported AI providers, feature sections (conversation analysis, sentiment scoring, topic detection, workflow automation, SDK integration), pricing tiers (Free through Enterprise), FAQ accordion, testimonials, and CTA sections.

## Steps

### Step 1

Navigate to the landing page at /

{{screenshot_1}}

### Step 2

Click the 'Sign Up' button in the top-right navigation header

{{screenshot_2}}

### Step 3

User is redirected to /auth/sign-up

{{screenshot_3}}

## Expected Outcome

User lands on the sign-up page with email, password, and confirm password fields.

## What Can Go Wrong

- Page may not load if server is down

## Related Flows

- [Email sign up](email-sign-up.md)
- [Social auth sign up](social-auth-sign-up.md)

## Navigation Path

```
http://localhost:3000 → / → [Navigate to sign up]
```
