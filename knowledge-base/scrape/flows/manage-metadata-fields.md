# Manage metadata fields

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Manage metadata fields |
| **Starting Page** | Analysis Config |
| **URL** | `/platform/[chatbotId]/analysis-config` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T09:34:43.182Z |

## Page Context

Configuration for conversation analysis with 5 tabs: Metadata, Translation, User Analysis, Assistant Analysis, Prompts

### Starting Page Screenshot

![Analysis Config](../screenshots/page-15.png)

## Business Purpose

This flow allows users to **manage metadata fields** from the Analysis Config page.

## Related Flows (Same Page)

- [Configure translation](configure-translation.md)
- [Configure user analysis](configure-user-analysis.md)
- [Configure assistant analysis](configure-assistant-analysis.md)
- [Edit prompts](edit-prompts.md)

## Available UI Elements

The following interactive elements are available on this page:

- tab: Metadata
- tab: Translation
- tab: User Analysis
- tab: Assistant Analysis
- tab: Prompts
- table: Managed fields (Key/Type/Status/Used/Discovered/Actions)
- table: Discovered fields (Key/Sample value/Occurrences)
- button: Track field

## Steps

### Step 1: Navigate to starting page

Navigate to `/platform/[chatbotId]/analysis-config` and verify the page loads correctly.

{{screenshot_1}}

### Step 2: Interact with tab: Metadata

Use the **tab: Metadata** element to progress through the flow.

{{screenshot_2}}

### Step 3: Interact with table: Managed fields (Key/Type/Status/Used/Discovered/Actions)

Use the **table: Managed fields (Key/Type/Status/Used/Discovered/Actions)** element to progress through the flow.

{{screenshot_3}}

### Step 4: Interact with table: Discovered fields (Key/Sample value/Occurrences)

Use the **table: Discovered fields (Key/Sample value/Occurrences)** element to progress through the flow.

{{screenshot_4}}

### Step 5: Verify outcome

Verify that the "Manage metadata fields" completed successfully and the expected state change occurred.

{{screenshot_5}}

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/analysis-config → [Manage metadata fields]
```

## Related Pages

- **Chatbot Settings** (`/platform/[chatbotId]/settings`) — Chatbot configuration with 6 tabs: General, Company Info, API Keys, Members, Webhooks, Import/Export
