# Manage metadata fields

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Manage metadata fields |
| **Starting Page** | Analysis Config |
| **URL** | `/platform/[chatbotId]/analysis-config` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Accept, deny, or track custom metadata keys sent by the SDK to control which fields appear as filters in the conversations table.

## Who Uses This

Developer or data team member configuring which SDK metadata fields are visible and filterable in the dashboard.

## Preconditions

- User is logged in
- SDK is sending conversations with custom metadata

## Page Context

Configuration page for how chatbot conversations are analyzed. Has five tabs: Metadata (managed fields and discovered fields with accept/deny/track controls), Translation, User Analysis, Assistant Analysis, and Prompts. The Metadata tab shows managed fields table (Key, Type, Status, Used, Discovered, Actions) and discovered fields table (Key, Sample value, Occurrences) with '+ Track' buttons to start tracking new metadata keys.

## Steps

### Step 1

Navigate to /platform/[chatbotId]/analysis-config

{{screenshot_1}}

### Step 2

The Metadata tab is selected by default

{{screenshot_2}}

### Step 3

Review 'Managed fields' to see currently tracked metadata keys and their status (Accepted/Denied)

{{screenshot_3}}

### Step 4

Review 'Discovered fields' for new metadata keys found in conversations

{{screenshot_4}}

### Step 5

Click '+ Track' on a discovered field to start managing it

{{screenshot_5}}

### Step 6

Click the X button on a managed field to remove it

{{screenshot_6}}

## Expected Outcome

Metadata fields are configured, and accepted fields become available as filters in the conversations and other tables.

## What Can Go Wrong

- No discovered fields if SDK isn't sending custom metadata

## Related Flows

- [Configure analysis settings](configure-analysis-settings.md)

## Navigation Path

```
http://localhost:3000 → /platform/[chatbotId]/analysis-config → [Manage metadata fields]
```
