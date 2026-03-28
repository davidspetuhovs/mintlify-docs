# Social auth login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Social auth login |
| **Starting Page** | `/auth/login` |
| **Persona** | User who prefers social login |

## Description

Authenticate using a social provider (Apple, Google, or Meta)

## Preconditions

- User has linked their social account

## Steps

### Step 1

Verify social auth buttons exist (Apple, Google, Meta)

### Step 2

Click Google social auth button

## Expected Outcome

User is authenticated and redirected to /platform

## Failure Modes

### Click social auth button in localhost without OAuth provider configured

Button click does not navigate — likely requires Supabase OAuth provider configuration

## Related Flows

- [Email login](email-login.md)

## Alternative Paths

- Email login
