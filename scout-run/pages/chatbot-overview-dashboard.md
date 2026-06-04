# Chatbot Overview Dashboard

## Overview

| Property | Value |
|----------|-------|
| **URL** | `/platform/[chatbotId]` |
| **Application** | http://openbat.dev/auth/login |
| **Discovered** | 2026-06-04T08:23:49.143Z |

## Description

Primary chatbot analytics dashboard with an AI chat interface ('What can I help you discover?'), quick-access command hints (tag entity, scope by plan, user/assistant analysis, scope by prompt), and summary cards: At-Risk Orgs, Performance (Resolution %, Quality Issues, AI Literacy), Activity (conversation count), and Risks (churn risks, yes-man, hallucinations). Each metric is clickable with sparkline charts.

## Who Uses This

Product managers, CS leads, or engineering leads who want an at-a-glance view of chatbot health and want to ask questions about their data.

## Preconditions

- User is authenticated
- Chatbot exists and has been onboarded
- Chatbot belongs to user's organization

## Page Context

Accessed by clicking a chatbot card from /platform. The primary workspace after selecting a chatbot. Sidebar switches to chatbot-specific navigation: Dashboard, Reports, Workflows, Prompt, Users, Conversations, Query Types, Deep Search, Analysis Config, Chatbot Settings.

## Key Actions

- Ask the AI chat any question about chatbot data
- View at-risk organizations
- Check performance metrics (resolution, quality, AI literacy)
- Monitor activity trends
- Review risk signals (churn, yes-man, hallucinations)
- Click any metric to drill down
- Access conversation history via History dropdown

## Expected Outcome

User gets a quick health check of their chatbot and can drill into any area of concern or ask AI-powered questions.

## Interactive Elements

- textbox: Message input (AI chat)
- button: Submit
- button: History dropdown
- cards: At-Risk Orgs/Performance/Activity/Risks with sparklines
- link: View all (organizations)

## Flows Starting Here

- [Ask AI about chatbot data](../flows/ask-ai-about-chatbot-data.md) — Use the built-in AI assistant to ask natural-language questions about conversation data, sentiment trends, user behavior, and more.

## Navigation Path

```
http://openbat.dev/auth/login → /platform/[chatbotId]
```
