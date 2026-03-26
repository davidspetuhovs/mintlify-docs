# Workflows

**Route:** `/platform/[chatbotId]/workflows`
**Route:** `/platform/[chatbotId]/workflows/[workflowId]`
**Auth:** Session required (manage actions require owner or admin)

Workflows close the loop between insight and action. Instead of manually checking the dashboard for problems, you define conditions once — and OpenBat fires alerts automatically whenever those conditions are met.

---

## What Is a Workflow?

A workflow is a **trigger → conditions → actions** chain that runs automatically every time a message is analyzed.

```
Trigger (new user message or assistant response)
  └── Condition set (AND/OR logic on analysis results)
        └── Actions (webhook calls, Slack alerts)
```

When all conditions in a workflow evaluate to true for a given message, all configured actions execute in parallel. Each execution is logged with its outcome.

---

## Workflows Tab

The main view. Lists all workflows for the current chatbot with:
- Workflow name and description
- Enabled / disabled toggle
- Trigger type (user message or assistant message)
- Last modified date
- Quick actions (edit, delete, toggle)

### Creating a Workflow

Click **Create Workflow** to open the workflow editor. Give it a name, description, and optionally start from a template.

---

## Workflow Editor

**Route:** `/platform/[chatbotId]/workflows/[workflowId]`

A visual node-based editor for building the trigger → condition → action graph.

### Trigger Node

Every workflow starts with a trigger that defines which messages activate it:

| Trigger Type | Activates On |
|-------------|-------------|
| User message | Every new user message after analysis completes |
| Assistant message | Every new assistant message after analysis completes |
| Any message | Both user and assistant messages |

### Condition Nodes

Zero or more condition nodes evaluate the analysis results for the triggering message. Conditions support AND/OR logic:
- **AND** — all conditions must be true
- **OR** — any condition must be true

Conditions compare analysis outputs against thresholds:

| Analysis Type | Comparable Fields | Operators |
|--------------|------------------|-----------|
| Sentiment | Score (numeric) | `>`, `<`, `>=`, `<=`, `=` |
| Sentiment | Label (string) | `=`, `!=` |
| Intent | Value (slug) | `=`, `!=` |
| Topic | Value (slug) | `=`, `!=` (any detected topic) |
| Flag | Value (slug) | `detected` / `not detected` |
| Behavior | Value (slug) | `=`, `!=` |
| Outcome | Value (slug) | `=`, `!=` |
| Quality dimension | Score (numeric) | `>`, `<`, `>=`, `<=` |

**Example conditions:**
- `sentiment score < -0.5` → very negative message
- `flag = churn_risk AND sentiment label = Negative` → high-confidence churn signal
- `outcome = capability_failure` → bot couldn't answer
- `behavior = hallucinating` → critical quality issue

### Action Nodes

When conditions pass, actions execute. Action types:

**Webhook (HTTP)** — POST to any URL with a configurable payload template. Variables interpolated from the message analysis:
- `{{user.name}}`, `{{user.email}}`
- `{{sentiment.score}}`, `{{sentiment.label}}`
- `{{intent.value}}`
- `{{conversation.id}}`

**Slack Webhook** — Sends a formatted Slack message via an incoming webhook URL. Uses the same template system with Slack-flavored markdown.

Webhooks are defined in the Webhooks settings tab and selected by name in the workflow editor.

---

## Runs Tab

The execution history for all workflows on this chatbot. Shows every time any workflow was evaluated, with:

| Column | Description |
|--------|-------------|
| Workflow | Which workflow ran |
| Status | `success` / `failed` / `skipped` |
| Matched conditions | The conditions that evaluated true |
| Actions executed | Which actions fired |
| Triggered at | Timestamp |

**Statuses:**
- `success` — conditions matched, actions executed successfully
- `failed` — conditions matched, but an action (webhook call) failed
- `skipped` — workflow evaluated but conditions didn't match (not logged unless explicitly enabled)

The runs tab is your debugging interface — when a webhook isn't firing as expected, check here to see whether the condition evaluation matched.

---

## Templates Tab

Pre-built workflow recipes for common use cases. Browse and apply a template to create a pre-configured workflow you can customize.

**Example templates:**
- **Churn Risk Alert** — Triggers when `churn_risk` flag detected + sentiment < −0.3. Action: Slack notification.
- **Capability Failure Tracker** — Triggers when `outcome = capability_failure`. Action: webhook to your issue tracker.
- **Hallucination Alert** — Triggers when `behavior = hallucinating`. Action: Slack urgent notification.
- **Buying Signal Alert** — Triggers when `buying_signal` flag detected. Action: webhook to CRM or Slack.
- **High-Frustration Escalation** — Triggers when sentiment < −0.5 AND intent = complaint. Action: Slack to CS channel.

---

## How Execution Works (Under the Hood)

Every time message analysis completes (sentiment, intent, topics, flags for user messages; behavior, outcome for assistant messages), the `executeWorkflows` step runs as part of the same Vercel Workflow DevKit pipeline:

1. Fetches all enabled workflows for the chatbot
2. Filters by trigger type (does this workflow care about user or assistant messages?)
3. Traverses the condition graph using BFS
4. Evaluates each condition node against the freshly computed analysis results
5. If all conditions pass: executes all action nodes in parallel
6. Logs the execution result (success/failed/skipped) to `workflow_executions`

This means workflow execution is **automatic** — there's no polling or cron. It fires within the same analysis pipeline, typically within seconds of the message being captured.

---

## Business Case

Workflows transform OpenBat from a passive analytics tool into an active early-warning system.

**Without workflows:** You check the dashboard periodically and hope you catch problems in time.

**With workflows:** You define what "a problem" looks like once, and your team is notified the moment it happens — while the conversation is still active or the user is still reachable.

**Highest-value workflow patterns:**
1. `churn_risk flag + sentiment < -0.4` → Slack CS channel → reach out same day
2. `behavior = hallucinating` → Slack engineering channel → investigate immediately
3. `outcome = capability_failure` → webhook to GitHub Issues → auto-creates a ticket
4. `buying_signal flag` → webhook to CRM → creates a deal or task for sales

Workflows are the difference between reactive damage control and proactive customer success.
