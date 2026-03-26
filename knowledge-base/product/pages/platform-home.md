# Platform Home

The platform home is your organization's control center — where you manage chatbots, invite teammates, and switch between orgs. Every chatbot you create lives here.

---

## Chatbot Grid
**Route:** `/platform`
**Auth:** Session required

Your primary landing page after login. Displays all chatbots in the current organization as a grid of cards, each showing the chatbot name and key stats.

**What you see:**
- All chatbots in the current org with conversation count and message totals
- Stat summary per chatbot card
- "Create chatbot" action to add a new one
- Organization switcher in the sidebar (if you belong to multiple orgs)

**What you can do:**
- Click any chatbot card to open its dashboard
- Create a new chatbot (prompts for a name, generates an API key shown once)
- Switch to a different organization via the sidebar

**Business case:** Teams often manage multiple chatbots (different products, regions, or environments). The grid gives you a fast overview of all chatbots and their relative activity at a glance.

**Auto-org creation:** First-time users who have no organization get one created automatically, named after their email prefix. No manual setup step.

---

## Organization Members
**Route:** `/platform/members`
**Auth:** Session required

Manage who has access to your organization. See current members with their roles, and invite new ones.

**What you see:**
- Table of all organization members: name, email, role (owner / admin / member), join date
- "Invite member" button (visible to owners and admins only)

**What you can do:**
- View all members and their roles
- Invite a new member by email (owners and admins)
- Remove members (owners and admins)

**Roles:**
| Role | Capabilities |
|------|-------------|
| **Owner** | Full access — can delete org, manage all members, all chatbots |
| **Admin** | Can invite/remove members, manage all chatbots |
| **Member** | Read and use access — cannot manage members or delete resources |

**Business case:** Product and CS teams often need read-only access to conversation insights without the ability to modify settings or rotate API keys. Role separation enforces that boundary cleanly.

---

## Organization Settings
**Route:** `/platform/settings`
**Auth:** Session required — owner or admin

Configure organization-level settings and manage the organization lifecycle.

**What you see:**
- Organization name form (owners only can edit)
- Danger Zone — delete organization permanently (owners only)

**What you can do:**
- Rename the organization
- Delete the organization (irreversible, cascades all chatbots and their data)

**Business case:** Organization name appears in the sidebar and is referenced in team invitations. The deletion path is intentionally gated to owner-only with a confirmation step to prevent accidental data loss.

---

## Sidebar Navigation

The main sidebar (visible on all `/platform/*` pages) provides:

**Org-level nav:**
- Platform home (chatbot grid)
- Members
- Settings
- Organization name and switcher (header)

**Chatbot-level nav** (when inside a chatbot):
- Dashboard
- Conversations
- Organizations (external)
- Users (external)
- Reports (with recent reports listed)
- Workflows
- Settings

**Footer:**
- Logged-in user name and email
- Sign out

---

## First-Time Onboarding Flow

When a user creates a new chatbot, they're guided through onboarding:

1. Chatbot is created → API key generated (shown **once**, copy it now)
2. Redirect to `/platform/[chatbotId]/onboarding` — SDK setup steps
3. User integrates SDK and sends at least one message
4. Marks onboarding complete → redirects to the chatbot dashboard

If a chatbot has not completed onboarding (`settings.onboarded !== true`), the dashboard redirects back to onboarding. If onboarding is already complete, the onboarding page redirects to the dashboard.
