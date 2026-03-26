# Expand FAQ answers

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Expand FAQ answers |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and CTAs

## Business Purpose

This flow allows users to **expand faq answers** from the Landing Page page.

## Related Flows (Same Page)

- [Sign up flow](sign-up-flow.md)
- [Login flow](login-flow.md)
- [View pricing plans](view-pricing-plans.md)
- [View code examples](view-code-examples.md)

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

### Step 2: Interact with link: FAQs (anchor)

Use the **link: FAQs (anchor)** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with button: FAQ accordions (5)

Use the **button: FAQ accordions (5)** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Expand FAQ answers" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → / → [Expand FAQ answers]
```
