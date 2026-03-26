# Conversations

The conversations section lets you browse, search, and filter every conversation your chatbot has had — and drill into any individual conversation to see the full message history with AI analysis overlaid on each message.

---

## Conversation List
**Route:** `/platform/[chatbotId]/conversations`
**Auth:** Session required

Your searchable, filterable record of every conversation. Built for investigation — find the exact conversations you need quickly, whether that's "all frustrated enterprise users from the US this week" or "high-MRR accounts asking about a specific feature."

### What You See

A paginated table of conversations with the following columns (sortable):

| Column | Description |
|--------|-------------|
| User | External user name and email |
| Organization | External org name (if provided) |
| Messages | Total message count in the conversation |
| Sentiment | Average sentiment score with label badge |
| Language | Detected language badge (shown when auto-translation is enabled and a non-primary language is detected) |
| Last active | When the last message was received |
| Started | When the conversation began |

### Filtering

The conversation list supports powerful multi-dimensional filtering:

**Free-text search** — searches across user name, email, user ID, and conversation ID.

**Faceted filters** (multi-select dropdowns):
- User plan (e.g., Free, Pro, Enterprise)
- User industry
- Organization plan
- Organization industry
- Organization ID (find all conversations from a specific customer)
- User ID (all conversations from a specific user)
- Device (desktop / mobile / tablet)
- Country
- Detected language (when auto-translation is enabled — filter by Spanish, French, etc.)

**Range filters** (min/max sliders or inputs):
- Message count (e.g., conversations with 5–20 messages)
- Average sentiment (e.g., only conversations with sentiment < −0.3)
- User MRR (e.g., conversations from users paying $500–$2000/month)
- Organization MRR

**Sorting:** Any column, ascending or descending. Default is last active, newest first.

**Pagination:** 20 rows per page by default, configurable up to 100.

### Business Case

The conversation list is your investigation tool. Typical use cases:
- "Which enterprise customers (org MRR > $1000) had negative sentiment this month?" → filter by MRR range + sentiment range
- "What are users in the US asking about on mobile?" → filter by country + device
- "Find all conversations from customer Acme Corp" → filter by org ID
- "What does a typical short conversation look like?" → filter by message count 1–3

---

## Conversation Detail
**Route:** `/platform/[chatbotId]/conversations/[id]`
**Auth:** Session required

The full transcript of a single conversation — with every AI analysis result overlaid inline. This is where you go to understand exactly what happened in a specific interaction.

### What You See

**Conversation header:**
- User name and email
- Organization name (if captured)
- Total message count
- Conversation start date

**Sentiment summary:**
- Average sentiment score with label
- Distribution of sentiment labels across user messages (e.g., "3 positive, 1 neutral, 2 negative")

**Full message thread:**
Messages displayed as a chat transcript (chronological, top to bottom):

For **user messages:**
- Message content (bubble)
- **Sentiment badge** — the sentiment label for this message (Positive / Neutral / Negative / Very Negative, etc.)
- Sentiment score (numeric)
- Sentiment reasoning — the LLM's explanation of why it assigned that score
- **Intent badge** — what the user intended (e.g., troubleshooting, feature_request)
- **Topic badges** — up to 3 topics extracted from the message
- **Flag badges** — any business signals detected (churn_risk, buying_signal, etc.)
- Chunk-level reasoning for each analysis type

For **assistant messages:**
- Message content (bubble)
- **Behavior badge** — how the assistant responded (helpful, dodging, verbose, etc.)
- **Outcome badge** — how the conversation ended from this response (fully_resolved, capability_failure, etc.)
- Quality dimensions (if available)
- **Flag badges** — any assistant-side flags

For **translated messages** (when auto-translation is enabled):
- Translated text shown by default with a "Translated from [language]" indicator
- A **translation toggle** button in the filter bar switches all messages between translated and original view
- Analysis highlight chunks (underlines, colored text) are only shown in translated view — since analysis ran on translated text, the chunks reference positions in the translated content
- Original view shows the raw message as written by the user

For **system messages:**
- Content displayed with a distinct system role indicator

### Business Case

The detail view is used for:
- **Debugging** — "Why did this conversation end with a capability failure?" Trace the exact exchange.
- **Quality review** — Spot-check specific interactions to validate LLM analysis accuracy.
- **CS investigation** — When a customer reports a bad experience, pull up the conversation and see exactly what happened and what the bot said.
- **Training data** — Identify high-quality (or problematic) conversations for future bot training.

### Navigation

A breadcrumb at the top links back to the conversation list, preserving your filter state.

---

## Analysis Badges Reference

| Badge Type | Applies To | Possible Values |
|-----------|-----------|----------------|
| Sentiment label | User messages | Very Positive, Positive, Neutral, Negative, Very Negative |
| Intent | User messages | Defined per chatbot (e.g., troubleshooting, feature_request, complaint) |
| Topics | User messages | 0–3 per message, defined per chatbot |
| Flags (user) | User messages | churn_risk, frustrated_user, buying_signal, competitor_mention, urgent_request, confused_user, + custom |
| Behavior | Assistant messages | helpful, hallucinating, dodging, yes_man, over_apologizing, redirecting, verbose, robotic, other |
| Outcome | Assistant messages | fully_resolved, partially_resolved, deflected, capability_failure, incorrect, other |
| Flags (assistant) | Assistant messages | Custom per chatbot |

Each badge is color-coded: green for positive signals, red for critical issues, amber for warnings, and gray/blue for informational labels.
