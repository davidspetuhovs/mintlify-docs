# Auto-Translation

Auto-translation lets you analyze conversations from users who write in any of 27 supported languages — without changing anything about your chatbot. OpenBat detects the language, translates the message to your primary language, and runs all analysis on the translated text. The original is always preserved.

---

## Why Translation Matters

If your chatbot serves international users, you're getting messages in Spanish, French, Japanese, and dozens of other languages. Without translation:
- Sentiment analysis produces inconsistent results across languages
- Intent classification may fail on non-English text
- Flag detection misses signals buried in foreign-language messages
- Deep Search only works for your primary language
- Your team can't read the conversations

With auto-translation enabled, every message is normalized to one language before analysis. Your dashboard, reports, workflows, and Deep Search all work as if every user spoke your language.

---

## How It Works

```
Message arrives (e.g., Spanish)
  ↓
Translation step detects language → "es" (Spanish)
  ↓
Language ≠ primary? → Translate to English
  ↓
Store: translated_content + detected_language + is_translated=true
Flag conversation: has_foreign_language=true, detected_language="es"
  ↓
Analysis runs on translated text (sentiment, intent, topics, flags)
  ↓
Embedding runs on translated text (Deep Search)
```

If the message is already in the primary language, the step is skipped (status: `skipped`) and analysis runs on the original content as normal.

---

## Enabling Translation

### During Chatbot Creation

When creating a new chatbot, select the **Primary language** from the dropdown. This defaults to English. Translation is not enabled by default — it only controls which language is considered "native."

### In Settings → Translation Tab

**Route:** `/platform/[chatbotId]/settings?tab=translation`

Three cards:

1. **Auto-translate messages** — master toggle (off by default). When enabled, all new incoming messages are language-detected and translated if needed.

2. **Primary language** — select from 27 supported languages. Messages in this language are not translated. Messages in any other language are translated to this language.

3. **How it works** — info card explaining behavior, cost, and that originals are preserved.

---

## Supported Languages

| Code | Language | Code | Language | Code | Language |
|------|----------|------|----------|------|----------|
| en | English | ja | Japanese | pl | Polish |
| es | Spanish | zh | Chinese | sv | Swedish |
| fr | French | ko | Korean | da | Danish |
| de | German | ar | Arabic | fi | Finnish |
| pt | Portuguese | hi | Hindi | no | Norwegian |
| it | Italian | ru | Russian | th | Thai |
| nl | Dutch | tr | Turkish | vi | Vietnamese |
| | | | | id | Indonesian |
| | | | | uk | Ukrainian |
| | | | | cs | Czech |
| | | | | ro | Romanian |
| | | | | el | Greek |
| | | | | he | Hebrew |

---

## What Gets Stored

### On each message

| Column | Description |
|--------|-------------|
| `translated_content` | The translated text (null if not translated) |
| `detected_language` | ISO 639-1 language code (e.g., `es`, `fr`) |
| `is_translated` | Boolean — whether translation was performed |

### On each conversation

| Column | Description |
|--------|-------------|
| `has_foreign_language` | True if any message was detected as non-primary |
| `detected_language` | The detected language code (for filtering) |

### On message_analyses

| Column | Description |
|--------|-------------|
| `translation_status` | `pending` → `processing` → `completed` / `skipped` / `failed` |
| `translation_error` | Error detail if failed |
| `translation_completed_at` | Timestamp of completion |

---

## Conversation List

When translation is enabled and conversations contain non-primary language messages:

- A **Language** column appears showing the detected language name (e.g., "Spanish") as a badge
- The **detected_language** column is available as a **faceted filter** — filter to show only Spanish conversations, only French, etc.
- This makes it easy to answer: "How many conversations are happening in Spanish?" or "What's the sentiment for our German-speaking users?"

---

## Conversation Detail

### Translation Toggle

A toggle button in the filter bar (next to the "View" button) switches between:

- **Translated** (default) — shows translated content with analysis highlights (underlines, colored chunks). Each translated message shows a "Translated from [language]" indicator.
- **Original** — shows the raw message as the user wrote it. Analysis highlights are hidden since chunk positions reference the translated text.

The toggle is global — it switches all messages in the conversation at once.

### Mobile

On mobile, the same toggle appears in the message list header bar.

---

## Interaction with Other Features

| Feature | Behavior with Translation |
|---------|--------------------------|
| **Sentiment Analysis** | Runs on translated text for consistent scoring across languages |
| **Intent Classification** | Runs on translated text — intents match your primary-language vocabulary |
| **Topic Detection** | Runs on translated text |
| **Flag Detection** | Runs on translated text — "churn risk" is detected regardless of language |
| **Assistant Analysis** | Assistant messages are also translated and analyzed |
| **Deep Search** | Embeddings use translated content — search in your primary language finds results from any language |
| **Workflows** | Conditions evaluate against translated text |
| **Conversation Highlights** | Chunk-level highlights only shown in translated view (positions reference translated text) |
| **Reports** | All metrics based on analysis of translated text |

---

## Cost & Performance

- Translation adds **one additional LLM call per non-primary-language message**
- Messages already in the primary language are detected but not translated (no extra cost)
- The translation step runs **before** analysis — it adds to the total pipeline latency but does not block the capture API response
- Translation uses the same Gemini model as other analysis steps and is logged to the `llm_calls` audit table with `purpose: "translation"`

---

## Business Case

- **International SaaS products** — analyze conversations from users worldwide in one dashboard, one language
- **Multilingual support teams** — CS teams can read every conversation without speaking the user's language
- **Consistent analytics** — sentiment and intent results are comparable across languages (no bias from language-specific phrasing)
- **Language distribution insights** — filter by language to understand which markets are most active or have the most issues
