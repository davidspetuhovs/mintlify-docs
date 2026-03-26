# Sign up flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Sign up flow |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and CTAs

## Business Purpose

This flow allows users to **sign up flow** from the Landing Page page.

## Related Flows (Same Page)

- [Login flow](login-flow.md)
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

### Step 2: Interact with link: Sign Up

Use the **link: Sign Up** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "Sign up flow" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → / → [Sign up flow]
```

## Related Pages

- **Sign Up Page** (`/auth/sign-up`) — Account creation form with email, password, confirm password, social auth options
