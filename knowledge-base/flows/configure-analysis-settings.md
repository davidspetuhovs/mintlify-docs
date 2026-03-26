# Configure analysis settings

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Configure analysis settings |
| **Starting Page** | Analysis Config |
| **URL** | `/platform/[chatbotId]/analysis-config` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Switch between the five configuration tabs (Metadata, Translation, User Analysis, Assistant Analysis, Prompts) to fine-tune how the AI analyzes conversations.

## Who Uses This

Technical user who wants to customize analysis behavior — for example, adjusting prompts, enabling translation, or modifying which user/assistant analysis signals are detected.

## Preconditions

- User is logged in

## Page Context

Configuration page for how chatbot conversations are analyzed. Has five tabs: Metadata (managed fields and discovered fields with accept/deny/track controls), Translation, User Analysis, Assistant Analysis, and Prompts. The Metadata tab shows managed fields table (Key, Type, Status, Used, Discovered, Actions) and discovered fields table (Key, Sample value, Occurrences) with '+ Track' buttons to start tracking new metadata keys.

## Steps

### Step 1

Navigate to /platform/[chatbotId]/analysis-config

{{screenshot_1}}

### Step 2

Click through the tabs: Metadata, Translation, User Analysis, Assistant Analysis, Prompts

{{screenshot_2}}

### Step 3

Configure settings in each tab as needed

{{screenshot_3}}

## Expected Outcome

Analysis configuration is updated and future message analysis uses the new settings.

## What Can Go Wrong

- Invalid configuration values

## Related Flows

- [Manage metadata fields](manage-metadata-fields.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/analysis-config → [Configure analysis settings]
```
