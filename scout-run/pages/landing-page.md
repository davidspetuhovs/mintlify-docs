# Landing Page

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Marketing homepage for OpenBat — positions the product as 'Google Analytics for AI chatbots.' Features hero section, problem/solution narrative, feature walkthroughs (ingest & analyze, prompt suggestions, stakeholder notifications, analytics), SDK integration code samples, FAQ, and CTA sections.

## Who Uses This

Prospective customers — product managers, engineering leads, and CS managers evaluating chatbot analytics tools.

## Preconditions

- None — public page accessible to anyone

## Page Context

Entry point for organic and paid traffic. Links to use cases, compare pages, security, contact, sign-in, and sign-up. Footer contains full sitemap of marketing pages.

## Key Actions

- Read value proposition and feature explanations
- Click 'Start listening' CTA to sign up
- Navigate to Use Cases or Compare pages for deeper evaluation
- View SDK code examples (Vercel AI SDK, TypeScript, Python, REST API)
- Expand FAQ accordion items
- Click 'Sign in' to access existing account

## Expected Outcome

Visitor understands what OpenBat does and either signs up or explores deeper marketing pages.

## Interactive Elements

- button: Start listening (CTA, appears 3x)
- button: Sign in
- dropdown: Use cases menu
- dropdown: Compare menu
- link: Security
- link: Contact
- tabs: SDK code examples
- accordion: FAQ items
- logo carousel: Works with (OpenAI, Claude, Gemini, etc.)

## Flows Starting Here

- [Sign up from landing page](../flows/sign-up-from-landing-page.md) — New visitor reads the landing page value prop and clicks the CTA to create an account, beginning their journey toward setting up chatbot analytics.

## Navigation Path

```
http://openbat.dev/auth/login → /
```
