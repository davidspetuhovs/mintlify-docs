# Users & Organizations

OpenBat separates analytics by the external entities you pass through the SDK — the end users who interact with your chatbot, and the organizations (companies/accounts) those users belong to. These pages let you browse, filter, and surface patterns at the entity level rather than the conversation level.

---

## External Users
**Route:** `/platform/[chatbotId]/users`
**Auth:** Session required

A filterable directory of every unique user your chatbot has interacted with. Each row represents a real person from your product — identified by the `user.id` you pass through the SDK.

### What You See

A paginated table of external users:

| Column | Description |
|--------|-------------|
| User | Name and email (from SDK metadata) |
| Plan | Subscription plan (e.g., Free, Pro, Enterprise) |
| Industry | User's industry (if provided) |
| Organization | Which org they belong to |
| Conversations | Total conversation count |
| Avg Sentiment | Their average sentiment score across all conversations |
| MRR | Monthly recurring revenue (if provided) |
| First seen | When their first conversation was captured |

### Filtering

**Free-text search** — user name, email, or user ID.

**Faceted filters:**
- Plan (multi-select)
- Industry (multi-select)
- Organization (specific org or any)

**Range filters:**
- Conversation count (min/max)
- Average sentiment (min/max) — find your most or least satisfied users
- MRR (min/max) — filter to high-value accounts

**Sorting:** Any column, ascending or descending.

### Business Case

The users view is built for CS and account management workflows:
- **Churn prevention:** Sort by sentiment ascending to find the most frustrated users — then filter by high MRR to prioritize who to call
- **Expansion targeting:** Filter by buying_signal flag (via conversations) + high sentiment to find expansion candidates
- **Segment analysis:** Filter by plan or industry to understand how different segments experience the chatbot
- **Account health:** For any user, see conversation volume + sentiment trend at a glance

---

## External Organizations
**Route:** `/platform/[chatbotId]/organizations`
**Auth:** Session required

The same concept as external users, but aggregated at the organization (company/account) level. One row per unique organization you've passed through the SDK.

### What You See

A paginated table of external organizations:

| Column | Description |
|--------|-------------|
| Organization | Name (from SDK metadata) |
| Plan | Org-level subscription plan |
| Industry | Org's industry |
| Users | Number of unique users from this org |
| Conversations | Total conversation count across all users |
| Avg Sentiment | Average sentiment across all org conversations |
| MRR | Monthly recurring revenue for this account |
| First seen | When the first conversation from this org was captured |

### Filtering

**Free-text search** — org name or org ID.

**Faceted filters:**
- Plan (multi-select)
- Industry (multi-select)

**Range filters:**
- Conversation count (min/max)
- User count (min/max) — find orgs with high adoption
- Average sentiment (min/max)
- MRR (min/max)

**Sorting:** Any column, ascending or descending.

### Business Case

Organizations is where account-level health becomes visible:
- **Account health scoring:** Sort by sentiment ascending, filter by org MRR > $X — find at-risk high-value accounts before they escalate
- **Adoption analysis:** Sort by user count or conversation count to find most and least engaged accounts
- **QBR prep:** Pull up any specific org to see their conversation volume, sentiment trend, and typical topics
- **Churn signals at account level:** One frustrated power user might not be a signal — but when an entire org's sentiment drops, that's an account-level risk

---

## Metadata Sourcing

Both pages are only as rich as the metadata you pass through the SDK. Fields like plan, industry, and MRR must be explicitly provided when calling `recordMessages()`:

```javascript
client.recordMessages({
  conversationId: "...",
  user: {
    id: "user_123",
    name: "Alice Johnson",
    email: "alice@acme.com",
    plan: "enterprise",
    industry: "fintech",
    mrr: 1500
  },
  organization: {
    id: "org_acme",
    name: "Acme Corp",
    plan: "enterprise",
    mrr: 5000,
    industry: "fintech"
  },
  messages: [...]
});
```

Fields not provided will appear as empty in the table and won't be available as filters. Richer metadata = richer filtering and sorting.

See the [SDK documentation](../sdk.md) for the full metadata schema.
