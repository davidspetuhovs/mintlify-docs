# Create workflow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Create workflow |
| **Starting Page** | Workflows |
| **URL** | `/platform/[chatbotId]/workflows` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Workflow automation page with Workflows/Runs/Templates tabs

## Business Purpose

This flow allows users to **create workflow** from the Workflows page.

## Available UI Elements

The following interactive elements are available on this page:

- button: Create workflow
- tab: Workflows
- tab: Runs
- tab: Templates

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/workflows` and verify the page loads correctly.

### Step 2: Interact with button: Create workflow

Use the **button: Create workflow** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with tab: Workflows

Use the **tab: Workflows** element to progress through the flow.

{{screenshot_3}}

### Step 4: Verify outcome

Verify that the "Create workflow" completed successfully and the expected state change occurred.

{{screenshot_4}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/workflows → [Create workflow]
```

## Related Pages

- **Dashboard - Chatbots List** (`/platform`) — Main authenticated dashboard showing all chatbots with card/list view toggle, status tabs (Active/Pe
