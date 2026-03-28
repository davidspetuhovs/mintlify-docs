# Investigate a dissatisfied user

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Investigate a dissatisfied user |
| **Starting Page** | `/platform/{chatbotId}` |
| **Persona** | Customer success manager investigating negative experiences |

## Description

Click through from dissatisfied user list to their conversations

## Preconditions

- User is logged in
- Chatbot has analyzed conversations
- Dissatisfied users exist

## Steps

### Step 1

Navigate to chatbot dashboard, see 'Most dissatisfied users' section

### Step 2

Click 'Investigate →' next to Riccardo G (score 4.1)

### Step 3

Conversations page loads but shows ALL conversations (116 rows), not filtered to user

## Expected Outcome

Conversations page opens filtered to show only that user's conversations

## Failure Modes

### URL has ?user= query param but table shows all conversations unfiltered

BUG: The user filter query parameter is not being applied — all 116 conversations shown instead of just Riccardo's

## Related Flows

- [View conversation detail](view-conversation-detail.md)
- [Filter conversations](filter-conversations.md)
