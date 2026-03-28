# Navigate to sign up from landing page

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Navigate to sign up from landing page |
| **Starting Page** | `/` |
| **Persona** | Prospective user who has read about OpenBat and wants to create a free account |

## Description

Find and click sign-up link from the landing page to create an account

## Preconditions

- User is not logged in
- User is on the landing page

## Steps

### Step 1

Visit the landing page and verify navigation links are visible

### Step 2

Click 'Sign Up' in the top navigation bar

### Step 3

Verify the sign-up page loads with the account creation form

## Expected Outcome

User lands on the sign-up page ready to create an account

## Failure Modes

### 'Start Free' and 'Get Started' buttons are placeholder links (#link)

Clicking 'Start Free' or most 'Get Started' buttons does not navigate — only nav 'Sign Up' and Free tier 'Get Started' work

## Related Flows

- [Email sign up](email-sign-up.md)
- [Social auth login](social-auth-login.md)

## Alternative Paths

- Click 'Get Started' on Free pricing tier (only one that works)
