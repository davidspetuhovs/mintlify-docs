# Forgot password flow

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Forgot password flow |
| **Starting Page** | `/auth/login` |
| **Persona** | User who has forgotten their password |

## Description

Navigate from login to password reset page

## Preconditions

- User has an existing account

## Steps

### Step 1

Navigate to /auth/login

### Step 2

Click 'Forgot your password?' link

### Step 3

Verify landing on password reset page with email field

## Expected Outcome

User lands on the password reset page to enter their email

## Related Flows

- [Password reset](password-reset.md)
- [Email login](email-login.md)
