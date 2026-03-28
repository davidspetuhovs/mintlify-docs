# Browse chatbot users

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Browse chatbot users |
| **Starting Page** | `/platform/{chatbotId}/users` |
| **Persona** | Customer success manager tracking individual user satisfaction |

## Description

View and filter individual chatbot users with sentiment data

## Preconditions

- User is logged in
- Chatbot has conversations with user metadata

## Steps

### Step 1

Navigate to users page — 26 rows with columns: User, Email, Organization, Plan, MRR, Conversations, Sentiment, Last Activity

## Expected Outcome

Sortable, filterable table of chatbot users

## Related Flows

- [Browse client organizations](browse-client-organizations.md)
- [Investigate a dissatisfied user](investigate-a-dissatisfied-user.md)
