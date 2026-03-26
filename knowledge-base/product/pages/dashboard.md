# Dashboard

**Route:** `/platform/[chatbotId]`
**Auth:** Session required

The dashboard is your daily command center — a real-time picture of how your chatbot and its users are doing. It has two analysis lenses: **User Analytics** (how users feel and what they want) and **Assistant Analytics** (how well your bot is performing).

---

## Overview Strip

Four headline metrics always visible at the top, regardless of which tab is active:

| Metric | What It Means |
|--------|--------------|
| **Total Conversations** | All conversations in the selected period with trend vs prior period |
| **Average Sentiment** | Weighted sentiment score (−1 to +1) with label and trend |
| **Resolution Rate** | % of conversations that ended resolved (fully or partially) with trend |
| **Messages Today** | Real-time activity — messages captured so far today |

Each metric shows a trend indicator (↑ / ↓) comparing the current period against the equivalent prior period, so you can see if things are improving or degrading.

---

## Filters

- **Tab:** User Analytics or Assistant Analytics
- **Period:** 7 days / 14 days / 30 days

Period selection affects all charts and tables on the page. The default is 30 days.

---

## User Analytics Tab

Answers: *Who are your most frustrated users? What are they asking about? What's driving dissatisfaction?*

### Sentiment Bands Over Time
A stacked area or line chart showing the daily breakdown of conversations by sentiment band:
- **Satisfied** (score > +0.2)
- **Neutral** (score between −0.2 and +0.2)
- **Dissatisfied** (score < −0.2)

Shows how sentiment composition is shifting day by day — is the dissatisfied band growing? Is a recent product change correlating with improved satisfaction?

### Dissatisfied Users
A ranked list of up to 8 users with the worst average sentiment in the current period.

For each user:
- Name and email
- Average sentiment score
- Conversation count
- Dissatisfaction score (composite ranking metric)

This is the "who to call" list. CS teams use this to proactively reach out before users churn.

### Top Frustrations
The topics most associated with negative sentiment conversations — ranked by frustration signal strength.

For each topic:
- Display name
- Occurrence count
- Trend % vs prior period (growing frustration vs shrinking)

Use this to identify the product areas or question types generating the most friction.

### Support Topics
All topics detected across the period — not just the negative ones. Shows the full distribution of what users are asking about, ranked by volume.

For each topic:
- Display name
- Count
- Trend % vs prior period
- Whether it's auto-discovered (new, not yet in your definition list) or predefined

Auto-discovered topics appear when the LLM encounters a recurring pattern not in your vocabulary yet — a useful signal that your topic list needs expanding.

---

## Assistant Analytics Tab

Answers: *How is your assistant actually performing? What behaviors is it exhibiting? Where is it failing?*

### Response Quality
A radar chart or dimension grid showing your assistant's quality across 6 dimensions, each scored 0–1:

| Dimension | Weight | What It Measures |
|-----------|--------|-----------------|
| **Relevance** | 25% | Does the response actually address what was asked? |
| **Completeness** | 25% | Does it cover all parts of the question? |
| **Clarity** | 20% | Is it easy to understand? |
| **Accuracy** | 15% | Is the information correct? |
| **Conciseness** | 10% | Is it appropriately succinct? |
| **Tone Match** | 5% | Does it match the user's register and tone? |

Shows the weighted overall score, the delta vs prior period, and the count of responses scoring below 0.35 (the "failing" threshold).

### Behavior Alerts
The most frequent problematic assistant behaviors, ranked by severity:

| Behavior | Severity |
|----------|---------|
| `hallucinating` | Critical |
| `dodging` | High |
| `yes_man` | High |
| `over_apologizing` | Medium |
| `redirecting` | Medium |
| `verbose` | Medium |
| `robotic` | Low |
| `helpful` | — (positive) |

For each behavior: count, trend %, and count of new instances this period. A growing `hallucinating` count is an immediate red flag.

### Resolution Outcomes
How conversations end, broken into 6 outcome categories with percentages and period-over-period deltas:

| Outcome | Description |
|---------|-------------|
| `fully_resolved` | User's question was answered completely |
| `partially_resolved` | Some but not all of the question was addressed |
| `deflected` | Assistant redirected user elsewhere without resolving |
| `capability_failure` | Bot encountered something it couldn't handle |
| `incorrect` | Bot gave a wrong answer |
| `other` | Doesn't fit above categories |

Resolution rate = `(fully_resolved + partially_resolved) / total`.

### Capability Gaps
Topics where the assistant most frequently reaches `capability_failure` — the things users ask for that the bot can't do.

For each gap:
- Topic name
- Request count
- Unique users affected
- Trend vs prior period

This is your product roadmap input: what capabilities are users asking for that you haven't built yet?

---

## Business Case

The dashboard is designed for two distinct review patterns:

**Daily health check (2 minutes):** Glance at the overview strip. Check if sentiment trend is moving in the right direction. Review behavior alerts for any critical issues.

**Weekly deep dive (15 minutes):** Switch between tabs. Identify growing frustrations. Review capability gaps for roadmap input. Export dissatisfied users list for CS outreach.

The two-tab structure separates concerns cleanly — user experience problems (sentiment, frustrations, topics) from assistant performance problems (quality, behaviors, outcomes) — so the right team can act on the right data.
