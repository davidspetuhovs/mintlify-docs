# Settings

Settings covers two levels: chatbot-specific configuration and organization-wide settings. Chatbot settings is the most complex section — it controls everything from your API key to the vocabulary the LLM uses when analyzing conversations.

---

## Chatbot Settings
**Route:** `/platform/[chatbotId]/settings`
**Auth:** Session required
**Tabs:** General · API Keys · Members · Metadata · Translation · User Analysis · Assistant Analysis · Webhooks

---

### General Tab

Core chatbot identity and lifecycle management.

**Chatbot Name**
- Edit the display name of the chatbot (appears in sidebar, dashboard headers, and reports)
- Changes saved immediately on submit

**API Key**
- Shows the API key prefix (`ob_live_xxxx...`) — the full key is never shown again after creation
- **Rotate Key** button generates a new API key and immediately invalidates the old one
  - The new full key is shown once — copy it immediately
  - Any SDK integrations using the old key will fail until updated
- **Delete Chatbot** — irreversible. Cascades and deletes all conversations, messages, and analysis data for this chatbot

---

### Metadata Tab

Configure the structured metadata fields your SDK integration passes through.

#### Metadata Field Schema

Define which custom fields your SDK sends via the `custom` parameter. The schema controls:
- What field names are valid
- What data types are expected (string, number, boolean)
- Whether a field is required

Example: if your chatbot is embedded in a multi-tenant SaaS app, you might define custom fields like `subscription_tier`, `trial_days_remaining`, or `feature_flags`.

#### Discovered Metadata Keys

OpenBat automatically discovers custom keys your SDK is already sending, even if they're not in your schema definition. Discovered keys appear here — you can promote them to your official schema or ignore them.

This gives you a "what's actually being sent" view alongside "what you've officially defined," making it easy to keep the schema in sync with your SDK integration.

---

### Translation Tab

Controls automatic language detection and translation for multilingual conversations.

**Auto-translate messages** — off by default. Toggle to enable.
- When enabled, every incoming message is language-detected using AI
- Messages not in your primary language are automatically translated
- All analysis (sentiment, intent, topics, flags, behavior, outcome) runs on the **translated text** for consistent results
- The original message is always preserved alongside the translation
- Adds one additional AI call per non-primary-language message

**Primary language** — defaults to English.
- Select from 27 supported languages (English, Spanish, French, German, Portuguese, Italian, Japanese, Chinese, Korean, Arabic, Hindi, Russian, and more)
- Messages already in the primary language are not translated (status: "skipped")
- This setting is also available during chatbot creation

**How translation interacts with other features:**
- **Conversation list:** Conversations with foreign language messages show a language badge (e.g., "Spanish") and can be filtered by detected language
- **Conversation detail:** A toggle button lets you switch between translated and original view. Analysis highlights only appear in translated view.
- **Deep Search:** Messages are embedded using translated content, so semantic search works consistently in your primary language
- **Workflows:** Workflow conditions evaluate against translated text

---

### Analysis Tab

The most powerful settings section. Controls what OpenBat analyzes and defines the vocabulary the LLM uses.

#### User-Side Analysis

**Sentiment Analysis** — on by default. Toggle to disable.
- Controls whether user messages receive sentiment scoring
- Disabling stops `user_sentiments` records from being created

**Intent Classification** — on by default. Toggle to disable.
- Controls intent detection per user message
- **Intent Definitions** — the list of intents the LLM can assign
  - Each definition has: slug (e.g., `troubleshooting`), display name, description
  - The LLM picks exactly one intent per user message from this list
  - If confidence < 0.35 on all known intents, the LLM may suggest a new one — which gets auto-added as a pending definition
  - **Generate Definitions** — AI-assisted: analyzes your recent conversations and suggests an intent vocabulary tailored to your chatbot's domain

**Topic Detection** — off by default (opt-in). Toggle to enable.
- Controls topic extraction per user message (up to 3 topics per message)
- **Topic Definitions** — the list of topics the LLM can assign
  - Same structure as intents: slug, display name, description
  - Auto-discovery: new topics are suggested when the LLM encounters patterns not in the list
  - **Generate Definitions** — AI-assisted topic vocabulary generation from your conversation history

**Flag Detection** — on by default. Toggle to disable.
- Controls business-signal detection per user message
- **Flag Definitions** — the list of flags the LLM can detect
  - Default system flags (always available): `churn_risk`, `frustrated_user`, `buying_signal`, `competitor_mention`, `urgent_request`, `confused_user`
  - Custom flags can be added per chatbot
  - Multiple flags can fire on a single message

#### Assistant-Side Analysis

**Behavior Classification** — on by default.
- Classifies every assistant message into one behavior category
- Fixed vocabulary (not customizable): `hallucinating`, `dodging`, `yes_man`, `over_apologizing`, `redirecting`, `verbose`, `robotic`, `helpful`, `other`

**Outcome Classification** — on by default.
- Classifies conversation outcome from assistant response perspective
- Fixed vocabulary: `fully_resolved`, `partially_resolved`, `deflected`, `capability_failure`, `incorrect`, `other`

**Response Quality** — on by default.
- Multi-dimension quality scoring per assistant message
- Fixed dimensions: relevance, completeness, clarity, accuracy, conciseness, tone_match

**Assistant Flag Detection** — off by default (opt-in).
- Same flag mechanism as user messages, but applied to assistant responses
- Useful for detecting specific response patterns you want to track

---

### Webhooks Tab

Define the webhook endpoints used by Workflows as action targets.

**Each webhook has:**
- Name (used to identify it in the workflow editor)
- URL (the endpoint to POST to)
- Type (`slack` for Slack incoming webhooks, `http` for generic HTTP)
- Enabled / disabled toggle

Webhooks defined here are available as selectable actions in all workflows for this chatbot. Centralizing webhook configuration means you update the URL in one place if it changes — all workflows using it automatically pick up the change.

---

### Access Tab

Control which organization members have access to this specific chatbot.

By default, all organization members have access to all chatbots in the org. The Access tab lets you restrict a chatbot to specific members — useful for:
- Client-facing chatbots where only the relevant account team should have access
- Sensitive internal chatbots with restricted visibility
- Different chatbots managed by different sub-teams

**What you see:**
- Current members with access (name, email, role)
- "Add member" action to grant access to an org member who doesn't have it yet

---

## Organization Settings

See [Platform Home → Organization Settings](./platform-home.md#organization-settings) for org-level configuration (rename org, delete org, manage team members).

---

## Settings Architecture Summary

| Tab | Controls | Who Can Edit |
|-----|---------|-------------|
| General | Name, API key, delete | Owner or Admin |
| API Keys | Key display, rotation | Owner or Admin |
| Members | Per-chatbot member access | Owner or Admin |
| Metadata | Custom field schema | Owner or Admin |
| Translation | Auto-translate toggle, primary language | Owner or Admin |
| User Analysis | Sentiment, intent, topics, flags toggles + definitions | Owner or Admin |
| Assistant Analysis | Behavior, outcome, quality, flags toggles + definitions | Owner or Admin |
| Webhooks | Webhook endpoints | Owner or Admin |
| Org name | Organization display name | Owner only |
| Org delete | Delete entire org | Owner only |
| Org members | Invite / remove members | Owner or Admin |
