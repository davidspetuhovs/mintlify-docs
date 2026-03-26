# Deep Search

Deep Search is a semantic search engine that spans every conversation your chatbot has ever had. Unlike keyword-based search, it understands meaning — searching for "billing problems" also surfaces messages about "I was overcharged" or "payment failed."

---

## Deep Search Page
**Route:** `/platform/[chatbotId]/deep-search`
**Auth:** Session required

### What You See

**Search input** — a full-width search bar at the top. Type a natural language query and press Enter.

**Results table** — a paginated table of matching messages with the following columns:

| Column | Description |
|--------|-------------|
| User | External user name and email |
| Message | The matching message content (truncated with ellipsis) |
| Sentiment | Sentiment badge for that specific message |
| Conversation | Link to the full conversation (jumps to the exact message) |
| Date | When the message was sent |

### How It Works

1. Every message captured by OpenBat is embedded into a vector representation using Google's text embedding model
2. When you search, your query is embedded using the same model
3. Results are ranked by semantic similarity — not keyword matching
4. Each result links directly to the conversation detail view, scrolled to the exact matching message (`?msg=` parameter)

### Semantic vs Keyword Search

| Query | Keyword Search | Deep Search |
|-------|---------------|-------------|
| "export feature" | Only finds messages containing "export feature" | Also finds "download CSV", "bulk export", "save as spreadsheet" |
| "frustrated about billing" | Requires exact words | Finds "I've been charged three times", "your pricing is confusing" |
| "competitor comparison" | Requires "competitor" in text | Finds "how does this compare to Intercom?", "Zendesk does this better" |

### Integration with Conversation Detail

From the conversation detail view, clicking the sparkle icon on any message bubble opens a contextual Deep Search shortcut. This pre-fills the search with that message's content, letting you quickly find similar messages across all conversations.

Results from Deep Search link back to the conversation detail view with the `?msg=` parameter, which scrolls to and highlights the matched message.

### Translation Interaction

When auto-translation is enabled, messages are embedded using their **translated content** (not the original). This means Deep Search works consistently in your primary language — searching in English will find semantically similar messages regardless of what language the user originally wrote in.

### Business Case

- "Find every conversation where a user asked about SSO" — even if they said "single sign-on", "SAML", or "enterprise login"
- "What are users saying about our new pricing?" — surfaces all related feedback across conversations
- "Find frustrated messages about the API" — combines semantic meaning with tone
- "Has anyone else reported this bug?" — search by the bug description in natural language
