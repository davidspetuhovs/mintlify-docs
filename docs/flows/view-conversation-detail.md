# View conversation detail

## Overview

| Property | Value |
|----------|-------|
| **Flow** | View conversation detail |
| **Starting Page** | `/platform/{chatbotId}/conversations` |
| **Persona** | Analyst reviewing specific customer interactions |

## Description

Open a conversation to see the full transcript with analysis annotations

## Preconditions

- User is logged in
- Chatbot has at least one conversation

## Steps

### Step 1

Navigate to conversations page (116 rows, paginated)

### Step 2

Click on Riccardo G's conversation row

### Step 3

Conversation detail loads with full transcript, per-message tags (Very Negative, Complaint, System Support and Feedback, Dodging, Deflected, brand voice violation), sidebar with sentiment score (-0.90), user info, org info, session data

## Expected Outcome

Full conversation with analysis annotations and metadata sidebar

## Related Flows

- [Filter conversations](filter-conversations.md)
- [Review message-level analysis](review-message-level-analysis.md)
