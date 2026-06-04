# Reports

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/platform/[chatbotId]/reports` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

AI-native reports page where users can create chat-driven dashboards. Offers pre-built templates (Customer Pulse, Sentiment Distribution, Risk Flags Leaderboard, Topics & Intents Overview) and the ability to create blank reports. Reports are built by chatting with AI which generates OpenUI widgets.

## Who Uses This

Team leads who want reusable dashboards and periodic reports on chatbot performance.

## Preconditions

- User is authenticated
- Chatbot belongs to user's organization

## Page Context

Accessed from the chatbot sidebar. Reports are distinct from the AI chat on the dashboard — they persist as reusable dashboards.

## Key Actions

- Browse report templates
- Create a blank report
- Open an existing report
- Create a new report with '+ New report'

## Expected Outcome

User creates or opens a report that visualizes chatbot data through interactive widgets.

## Interactive Elements

- button: New report
- cards: template cards (Customer Pulse, Sentiment Distribution, etc.)
- button: Create a blank report
- link: Browse all templates

## Flows Starting Here

- [Create report from template](../flows/create-report-from-template.md) — Start a new report from a pre-built template to quickly get a populated dashboard with relevant widgets.

## Navigation Path

```
http://openbat.dev/auth/login → /platform/[chatbotId]/reports
```
