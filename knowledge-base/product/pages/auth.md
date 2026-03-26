# Authentication Pages

The auth section handles all user identity flows: creating accounts, signing in, recovering access, and verifying email. All pages are public (no session required) and render a centered single-card layout.

---

## Pages

### Login
**Route:** `/auth/login`

The entry point for returning users. Renders a login form that authenticates against Supabase Auth using email + password. On success, the user is redirected to `/platform` (their chatbot grid).

**What you see:**
- Email + password fields
- Submit button
- Links to sign-up and forgot password flows

---

### Sign Up
**Route:** `/auth/sign-up`

New user registration. Submits email + password to Supabase Auth, which sends a confirmation email. On submit, redirects to the sign-up success confirmation page.

**What you see:**
- Email + password fields
- Submit button
- Link back to login

**Post-sign-up:** User receives a confirmation email. Clicking the link routes through `/auth/confirm` which verifies the OTP token and redirects to `/platform`.

**First platform visit:** When a newly confirmed user hits `/platform` for the first time with no organization, OpenBat automatically creates an organization named after their email prefix. No manual setup required.

---

### Sign Up Success
**Route:** `/auth/sign-up-success`

Confirmation screen shown immediately after registration form submission. Purely informational — no actions available.

**What you see:**
- "Thank you for signing up!" heading
- Instruction to check email for confirmation link

---

### Forgot Password
**Route:** `/auth/forgot-password`

Initiates the password recovery flow. User enters their email address; Supabase sends a recovery link.

**What you see:**
- Email field
- Submit button

---

### Update Password
**Route:** `/auth/update-password`

Accessed via the link in the Supabase password recovery email. Allows the user to set a new password.

**What you see:**
- New password field (with confirmation)
- Submit button

---

### Auth Error
**Route:** `/auth/error?error=<message>`

Catch-all error display page for auth failures (expired tokens, invalid OTP, etc.). Reads the `error` query parameter from the URL and displays it in a card.

**What you see:**
- Error message from query parameter
- No actions (informational only)

---

### Email Confirmation Callback
**Route:** `/auth/confirm` (API route, not a UI page)

Handles the OTP token verification when a user clicks their confirmation email. Reads `token_hash`, `type`, and `next` from query parameters, verifies with Supabase, and redirects to the `next` URL on success or `/auth/error` on failure.

This route is not visited directly — it's the target URL embedded in Supabase's confirmation email links.

---

## Auth Flow Summary

```
Sign Up → /auth/sign-up-success (check email) → confirmation email →
  /auth/confirm (OTP verification) → /platform (auto-org creation)

Login → /auth/login → /platform

Forgot Password → /auth/forgot-password → email →
  /auth/update-password → /auth/login
```

---

## Access Control

Auth pages are the only routes that do **not** require a session. All `/platform/*` routes are protected — unauthenticated requests are redirected to `/auth/login` via the Next.js `proxy.ts` handler.
