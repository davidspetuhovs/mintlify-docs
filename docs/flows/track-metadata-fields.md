# Track metadata fields

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Track metadata fields |
| **Starting Page** | `/platform/{chatbotId}/analysis-config` |
| **Persona** | Developer who has set up SDK with custom metadata |

## Description

Accept discovered metadata fields to make them filterable

## Preconditions

- SDK is sending custom metadata
- Discovered fields appear in table

## Steps

### Step 1

Metadata tab shows Managed fields (custom.templateId, custom.templateName) and 8 Discovered fields (browser, custom.chatbot, device, ip, language, os, referer, userAgent) with Track buttons

## Expected Outcome

Tracked fields become available as filter columns in conversations table

## Related Flows

- [Filter conversations](filter-conversations.md)
