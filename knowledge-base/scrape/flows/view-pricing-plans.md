# View pricing plans

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View pricing plans |
| **Starting Page** | Landing Page |
| **URL** | `/` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Public marketing page with hero, features, pricing (6 tiers), FAQs, testimonials, code examples, and CTAs

## Business Purpose

This flow allows users to **view pricing plans** from the Landing Page page.

## Related Flows (Same Page)

- [Sign up flow](sign-up-flow.md)
- [Login flow](login-flow.md)
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

### Step 2: Interact with link: Pricing (anchor)

Use the **link: Pricing (anchor)** element to progress through the flow.

{{screenshot_2}}

### Step 3: Verify outcome

Verify that the "View pricing plans" completed successfully and the expected state change occurred.

{{screenshot_3}}

## Navigation Path

```
http://localhost:3000 → / → [View pricing plans]
```

## Related Pages

- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
- **Chatbot Dashboard** (`/platform/[chatbotId]`) — Overview dashboard with stats (conversations, messages, avg sentiment, analyzed today), date range s
- **Conversation Detail** (`/platform/[chatbotId]/conversations/[id]`) — Chat bubble view of a conversation with right sidebar showing overall sentiment, conversation metada
