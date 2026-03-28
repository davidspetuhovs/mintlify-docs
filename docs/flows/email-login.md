# Email login

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Email login |
| **Starting Page** | `/auth/login` |
| **Persona** | Returning user who already has an account |

## Description

Authenticate using email and password

## Preconditions

- User has an existing account
- User is not already logged in

## Steps

### Step 1

Navigate to /auth/login and verify the login form is visible

### Step 2

Enter email address in the Email field

### Step 3

Enter password in the Password field

### Step 4

Click 'Login' button

### Step 5

Verify redirect to /platform dashboard with chatbots visible

## Expected Outcome

User is redirected to /platform and sees their dashboard with chatbots

## Failure Modes

### Submit form with wrong password

Alert shown: 'Invalid login credentials' — stays on /auth/login

## Related Flows

- [Forgot password flow](forgot-password-flow.md)
- [Email sign up](email-sign-up.md)

## Alternative Paths

- Social auth login (Google/Apple/Meta)
