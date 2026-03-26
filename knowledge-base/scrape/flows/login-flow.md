# Login flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Login flow |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and CTAs

## Business Purpose

This flow allows users to **login flow** from the Landing Page page.

## Related Flows (Same Page)

- [Sign up flow](sign-up-flow.md)
- [View pricing plans](view-pricing-plans.md)
- [View code examples](view-code-examples.md)
- [Expand FAQ answers](expand-faq-answers.md)

## Available UI Elements

The following interactive elements are available on this page:

- link: Features (anchor)
- link: Pricing (anchor)
- link: FAQs (anchor)
- link: Login
- link: Sign Up
- button: Start Free
- button: Book a Demo
- tabs: Vercel AI SDK / TypeScript / Python / REST API
- button: FAQ accordions (5)
- button: Missed Upsell / Feature Gap Risk / Bot Hallucination

## Steps

### Step 1: Navigate to starting page

Navigate to `/` and verify the page loads correctly.

### Step 2: Interact with link: Login

Use the **link: Login** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Login flow" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → / → [Login flow]
```

## Related Pages

- **Login Page** (`/auth/login`) — Email/password login with social auth (Apple, Google, Meta) and forgot password link
