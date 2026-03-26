# Product Overview

## What Is OpenBat?

OpenBat is a **conversational analytics platform** for SaaS companies that deploy AI chatbots. It answers the questions your conversation logs can't: What are users actually frustrated about? Where does your assistant fail? Which users are about to churn?

You drop in the SDK, conversations start flowing, and OpenBat's LLM analysis pipeline extracts business-critical signals from every message — automatically, without any manual tagging or categorization.

---

## The Problem It Solves

AI chatbots generate thousands of conversations a day. Almost none of that data gets actioned.

The typical workflow: logs exist, nobody reads them. When something goes wrong — rising support volume, churning users, a broken assistant — teams find out through tickets, customer calls, or executive escalations. By then it's too late.

OpenBat closes the loop between "chatbot runs" and "team knows what's happening." It transforms raw conversation streams into structured intelligence:

- Which users are dissatisfied right now
- What topics are driving frustration
- Where the assistant is failing (hallucinating, dodging, giving incomplete answers)
- Which conversations represent buying signals vs churn risks
- Whether your assistant is improving or degrading over time

---

## Who It's For

### Primary Users
**Product managers and engineering leads** who own an AI chatbot product. They visit OpenBat to understand what customers are asking, how the bot is responding, and where to focus improvement effort.

**Customer success teams** who need to identify at-risk users early — before they escalate or churn — and proactively reach out.

**AI/ML engineers** tuning chatbot behavior. They use OpenBat to measure response quality across dimensions (relevance, accuracy, clarity) and detect behavioral regressions.

### Organizational Context
Teams that:
- Ship a product with an embedded AI assistant or chatbot
- Have enough conversation volume to need analytics (1,000+ conversations/month)
- Want structured insight without building their own analytics infrastructure
- Need alerting when specific patterns emerge (churn signals, capability failures)

---

## Core Value Propositions

### 1. Instant Signal from Noise
Every user message is analyzed for sentiment, intent, topics, and business flags — automatically. No manual tagging. No labeling pipelines. You connect the SDK and insights start appearing within minutes.

### 2. Both Sides of the Conversation
Most analytics tools look at one side. OpenBat analyzes both:
- **User-side:** what they want, how they feel, what's frustrating them
- **Assistant-side:** how well it's responding, what behaviors it exhibits, whether it actually solved the problem

### 3. Business Intelligence, Not Just Metrics
OpenBat doesn't stop at "average sentiment is 0.4." It surfaces:
- The 8 users with lowest satisfaction right now
- The topics correlating with dissatisfaction
- Capability gaps — where users ask for things the bot can't do
- Resolution rates — what percentage of conversations end resolved vs deflected

### 4. Act on What You Find
Insights are only useful if they trigger action. Workflows close the loop: define a condition (e.g., "churn risk flag detected + sentiment < -0.5"), connect a webhook, and your team gets a Slack notification the moment it fires.

### 5. Your Vocabulary, Your Rules
Intent, topic, and flag definitions are fully customizable per chatbot. OpenBat auto-discovers new categories when the LLM encounters patterns your list doesn't cover — and adds them with your approval.

### 6. Deep Search Across Every Conversation
Semantic search that understands meaning, not just keywords. Search for "billing problems" and find messages about "I was overcharged" or "payment failed." Results link directly to the exact message in the conversation, with full analysis context.

### 7. Multilingual Out of the Box
Enable auto-translation and OpenBat handles 27 languages automatically. Messages are detected, translated to your primary language, and analyzed on the translated text — while preserving the original. Filter conversations by language, toggle between original and translated in one click, and get consistent analysis regardless of what language your users write in.

---

## Competitive Positioning

OpenBat sits between:
- **Generic analytics tools** (Amplitude, Mixpanel) — too general, no conversation-native features
- **Custom LLM pipelines** — too expensive and slow to build, nothing to show for it
- **Conversation review tools** (Intercom, Zendesk analytics) — focused on human support, not AI chatbot intelligence

OpenBat is purpose-built for AI chatbot teams who need conversation intelligence without building it themselves.

---

## Key Metrics OpenBat Tracks

| Metric | Description |
|--------|-------------|
| Total conversations | Volume across any date range |
| Average sentiment | Weighted −1 to +1 score |
| Resolution rate | % of conversations marked fully or partially resolved |
| Churn risk count | Conversations where churn_risk flag fired |
| Buying signal count | Conversations with buying_signal flag |
| Messages today | Real-time activity indicator |
| Sentiment trend | Daily sentiment trajectory over 7/14/30 days |
| Sentiment bands | % satisfied / neutral / dissatisfied per day |
| Top frustrations | Topics clustering around negative sentiment |
| Response quality | 6-dimension score per assistant message |
| Behavior frequency | Count of each assistant behavior type |
| Capability gaps | Topics where assistant outcome = capability_failure |

---

## Product Architecture (Non-Technical Summary)

1. **SDK** — Tiny JavaScript client that captures messages from your chatbot and sends them to OpenBat's API
2. **Ingestion API** — Validates API keys, deduplicates messages, stores conversations with metadata
3. **Analysis Pipeline** — Durable LLM workflows run on every new message, extracting structured signals
4. **Dashboard** — Aggregated analytics, filtered views, and custom reports built from analysis output
5. **Workflows** — Condition-based automation that fires webhooks when defined patterns are detected

Everything runs on Vercel (functions, workflow execution) with Supabase as the data layer. The LLM backend is Google Gemini via the direct Google GenAI SDK.
