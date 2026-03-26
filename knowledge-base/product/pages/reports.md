# Reports

**Route:** `/platform/[chatbotId]/reports` → redirects to most recent report
**Route:** `/platform/[chatbotId]/reports/[reportId]`
**Auth:** Session required

Reports are fully customizable dashboards — a configurable canvas of widgets pulled from the same analytics data that powers the main dashboard. Build a report once, share the URL with your team, adjust the time range on the fly.

---

## What Is a Report?

A report is a named, saved layout of widgets. Each report has:
- A **name** (shown in the sidebar)
- A **default time range** (days, 1–90)
- An ordered **grid of widgets**, each with a size (third, half, or full width)

Reports are listed in the sidebar under the chatbot navigation. Clicking a report opens it directly. The most recently updated report is where you land when navigating to `/reports`.

---

## Creating a Report

From the reports index (or the sidebar "+" button):
1. Click **Create Report**
2. Give it a name and choose a default time period
3. The report opens as an empty canvas
4. Add widgets from the widget library
5. Arrange and size widgets to taste
6. Save

---

## Widget Library

Reports support 14 widget types, organized into three categories:

### Stat Widgets
Headline numbers, each showing the value + trend vs the prior equivalent period:

| Widget | What It Shows |
|--------|--------------|
| `stat_total_conversations` | Total conversations in the period |
| `stat_avg_sentiment` | Average sentiment score + label |
| `stat_resolution_rate` | % of conversations resolved (fully or partially) |
| `stat_churn_risk_count` | Conversations with a churn_risk flag |
| `stat_buying_signal_count` | Conversations with a buying_signal flag |
| `stat_messages_today` | Real-time count of messages received today |

All stat widgets display trend indicators (↑↓) comparing current to prior period.

### Chart Widgets
Visualizations for time-series and distribution data:

| Widget | What It Shows |
|--------|--------------|
| `chart_sentiment_trend` | Daily average sentiment score over time (line chart) |
| `chart_conversation_volume` | Daily conversation count over time (bar chart) |
| `chart_intent_distribution` | Breakdown of intents by count and % (bar or donut) |
| `chart_sentiment_distribution` | Count of each sentiment label (bar or donut) |
| `chart_flag_distribution` | Count of each flag type fired (bar chart) |
| `chart_outcome_distribution` | Resolution outcome breakdown (donut or bar) |

### List Widgets
Ranked tables showing top items:

| Widget | What It Shows |
|--------|--------------|
| `list_top_topics` | Top 10 topics by volume in the period |
| `list_recent_conversations` | 8 most recent conversations with user + sentiment |

---

## Widget Sizing

Each widget occupies a fraction of the report grid row:

| Size | Grid Columns | Use For |
|------|-------------|---------|
| `third` | 1/3 width | Stat widgets, compact lists |
| `half` | 1/2 width | Charts, medium tables |
| `full` | Full width | Wide charts, detailed tables |

Widgets reflow responsively — full-width on mobile regardless of size setting.

---

## Time Range Control

The default time range is set per report (in the report config). When viewing a report, a day-range selector lets you override it on the fly without changing the report's default. This means:
- One report can serve as both a "30-day view" and a "7-day view" — just adjust the selector
- Sharing a URL with `?days=7` overrides the default for that view session
- The report's saved default isn't changed by URL overrides

---

## Query Deduplication

When a report has multiple widgets of the same type (e.g., two stat widgets), OpenBat batches the underlying queries — running one query per unique widget type regardless of how many instances exist. This keeps report loading fast even for complex multi-widget layouts.

---

## Report Sidebar Navigation

Reports appear in the chatbot sidebar under "Reports," showing up to 6 recent reports by name. A "View all" link shows the full list. Reports can be created from the sidebar "+" button.

---

## Business Case

Reports exist for two scenarios:

**Stakeholder reporting:** Build a weekly exec report with the 3–4 metrics leadership cares about (conversations, sentiment trend, resolution rate, top topics). Share the link. They can adjust the time range themselves without needing to understand the full platform.

**Team-specific views:** A CS team might want a "At-Risk Accounts" report showing churn risk count + frustrated users + low sentiment conversations. Engineering wants a "Bot Health" report with behavior alerts + capability gaps + resolution outcomes. One platform, multiple stakeholders, each with their own view.

Reports also serve as a way to track focused metrics over time — create a report for a specific initiative (e.g., "New feature launch — user reception") and watch the relevant widgets over the rollout period.
