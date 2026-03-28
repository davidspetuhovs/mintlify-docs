# Review message-level analysis

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Review message-level analysis |
| **Starting Page** | `/platform/{chatbotId}/conversations/{conversationId}` |
| **Persona** | QA analyst investigating AI analysis decisions |

## Description

View detailed AI analysis tags on individual messages

## Preconditions

- User is on a conversation detail page
- Messages have been analyzed

## Steps

### Step 1

On conversation detail, clickable analysis tags visible on messages: 'Very Negative', 'Complaint', 'System Support and Feedback' (user), 'Dodging', 'Deflected', 'brand voice violation' (assistant)

## Expected Outcome

Analysis tags are clickable and show reasoning for each annotation

## Related Flows

- [View conversation detail](view-conversation-detail.md)
