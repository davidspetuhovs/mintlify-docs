# Password reset

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Password reset |
| **Starting Page** | `/auth/forgot-password` |
| **Persona** | User who has forgotten their password |

## Description

Request a password reset email

## Preconditions

- User has an existing account with a valid email

## Steps

### Step 1

Navigate to /auth/forgot-password

### Step 2

Enter email and click 'Send reset email'

### Step 3

Verify confirmation message: 'Check Your Email'

## Expected Outcome

Confirmation page: 'Password reset instructions sent'

## Related Flows

- [Forgot password flow](forgot-password-flow.md)
- [Email login](email-login.md)
