# Create workflow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Create workflow |
| **Starting Page** | Workflows |
| **URL** | `/platform/[chatbotId]/workflows` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Set up an automated workflow that triggers alerts or actions when specific analysis conditions are met (e.g., negative sentiment detected, churn risk flagged).

## Who Uses This

CS lead or ops manager who wants automated alerts when important patterns are detected in chatbot conversations.

## Preconditions

- User is logged in
- Chatbot exists

## Page Context

Workflow automation page for creating alert and action workflows that trigger based on conversation analysis conditions. Has three tabs: Workflows (list of configured workflows), Runs (execution history), and Templates (pre-built workflow templates). Shows empty state with 'Create workflow' button when no workflows exist.

## Steps

### Step 1

Navigate to /platform/[chatbotId]/workflows

{{screenshot_1}}

### Step 2

Click the '+ Create workflow' button

{{screenshot_2}}

### Step 3

Configure trigger conditions (e.g., sentiment threshold, specific behavior detected)

{{screenshot_3}}

### Step 4

Set up actions (e.g., Slack alert, email notification)

{{screenshot_4}}

### Step 5

Save the workflow

{{screenshot_5}}

## Expected Outcome

A new workflow is created and will automatically trigger when its conditions are met during message analysis.

## What Can Go Wrong

- Plan limit on number of workflows reached
- Invalid workflow configuration

## Related Flows

- [View workflow runs](view-workflow-runs.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/workflows → [Create workflow]
```
