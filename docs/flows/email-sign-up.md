# Email sign up

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Email sign up |
| **Starting Page** | `/auth/sign-up` |
| **Persona** | New user who wants to create an account |

## Description

Create a new account with email and password

## Preconditions

- User does not have an existing account
- User is not logged in

## Steps

### Step 1

Navigate to /auth/sign-up and verify form fields

### Step 2

Enter email, password, and confirm password

### Step 3

Click 'Create Account'

## Expected Outcome

Account is created and user is redirected to the platform

## Failure Modes

### Password too short (less than 6 characters)

Alert: 'Password should be at least 6 characters.' Note: UI says 8 but backend enforces 6

### Passwords don't match

Alert: 'Passwords do not match'

### Email already registered

Alert: 'User already registered'

## Related Flows

- [Email login](email-login.md)
- [Navigate to sign up from landing page](navigate-to-sign-up-from-landing-page.md)

## Alternative Paths

- Social auth sign up (Apple/Google/Meta)
