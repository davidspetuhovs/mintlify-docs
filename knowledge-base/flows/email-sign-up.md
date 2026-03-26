# Email sign up

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Email sign up |
| **Starting Page** | Sign Up Page |
| **URL** | `/auth/sign-up` |
| **Application** | http://localhost:3000 |
| **Discovered** | 2026-03-26T16:31:25.553Z |

## Description

Create a new OpenBat account using email and password. After sign-up, the user's organization is auto-created on first visit to the platform.

## Who Uses This

New user who has decided to try OpenBat and wants to create an account to start analyzing their chatbot conversations.

## Preconditions

- User does not have an existing account
- User has a valid email address

## Page Context

Account creation page for new users. Features a split layout with a registration form on the left and a decorative image on the right. Requires email, password, and password confirmation. Also supports social sign-up via Apple, Google, and Meta. Includes a link to sign in for existing users.

## Steps

### Step 1

Navigate to /auth/sign-up

{{screenshot_1}}

### Step 2

Enter email address in the Email field

{{screenshot_2}}

### Step 3

Enter a password (at least 8 characters) in the Password field

{{screenshot_3}}

### Step 4

Re-enter the same password in the Confirm Password field

{{screenshot_4}}

### Step 5

Click the 'Create Account' button

{{screenshot_5}}

### Step 6

Wait for account creation and redirect

{{screenshot_6}}

## Expected Outcome

Account is created. User is redirected to /platform where their organization is auto-created (named after their email prefix). They see an empty chatbot list and can create their first chatbot.

## What Can Go Wrong

- Email already in use shows an error
- Password too short (under 8 characters)
- Passwords don't match
- Invalid email format

## Related Flows

- [Email login](email-login.md)
- [Create new chatbot](create-new-chatbot.md)

## Navigation Path

```
http://localhost:3000 → /auth/sign-up → [Email sign up]
```
