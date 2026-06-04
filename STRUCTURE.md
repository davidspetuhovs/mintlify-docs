# OpenBat docs — structure (scaffolding pass)

Generated structure-only scaffold. **78 pages**, **65 images mapped**, **6 tabs**. No prose written yet — every page is a stub with frontmatter, a SOURCES comment, wired `<Frame>` image placeholders, and a `{/* TODO: write content */}` marker.

## Navigation tree

```
Get started/   (tab, icon: rocket)
  Overview/
    - Introduction  (index.mdx)
    - Quickstart  (get-started/quickstart.mdx)  [1 img]
    - How OpenBat works  (get-started/how-openbat-works.mdx)
    - Core concepts  (get-started/concepts.mdx)
    - Ways to use OpenBat  (get-started/surfaces.mdx)
Platform/   (tab, icon: layout-dashboard)
  Guides/
    - Sign up from the landing page  (platform/guides/sign-up-from-landing-page.mdx)  [4 img]
    - Create your account  (platform/guides/email-sign-up.mdx)  [5 img]
    - Log in  (platform/guides/email-login.mdx)  [4 img]
    - Reset your password  (platform/guides/password-reset-request.mdx)  [4 img]
    - Create a chatbot  (platform/guides/create-new-chatbot.mdx)  [2 img]
    - Explore a demo chatbot  (platform/guides/explore-demo-chatbot.mdx)  [2 img]
    - Invite a team member  (platform/guides/invite-team-member.mdx)  [2 img]
    - Ask AI about your data  (platform/guides/ask-ai-about-chatbot-data.mdx)  [1 img]
    - Create a report from a template  (platform/guides/create-report-from-template.mdx)  [2 img]
    - Create a workflow from a template  (platform/guides/create-workflow-from-template.mdx)  [3 img]
    - Create a prompt version  (platform/guides/create-new-prompt-version.mdx)  [2 img]
    - Review a conversation  (platform/guides/review-a-specific-conversation.mdx)  [2 img]
    - Configure analysis  (platform/guides/configure-analysis-definitions.mdx)  [2 img]
    - Export conversation data  (platform/guides/export-conversation-data.mdx)  [2 img]
  Features/
    - Managing chatbots  (platform/features/managing-chatbots.mdx)  [8 img]
    - Overview dashboard  (platform/features/overview-dashboard.mdx)  [4 img]
    - Conversations  (platform/features/conversations.mdx)  [2 img]
    - Deep search  (platform/features/deep-search.mdx)  [1 img]
    - Query types  (platform/features/query-types.mdx)  [1 img]
    - Users & organizations  (platform/features/users-and-organizations.mdx)  [2 img]
    - AI reports  (platform/features/reports.mdx)  [1 img]
    - Workflows  (platform/features/workflows.mdx)  [1 img]
    - System prompt management  (platform/features/system-prompt.mdx)  [1 img]
    - Analysis configuration  (platform/features/analysis-config.mdx)  [1 img]
    - Team & access  (platform/features/team-and-access.mdx)  [3 img]
    - Chatbot settings  (platform/features/chatbot-settings.mdx)  [1 img]
    - Chatbot onboarding  (platform/features/onboarding.mdx)  [1 img]
  Reference/
    - Architecture  (platform/reference/architecture.mdx)
    - Page map  (platform/reference/page-map.mdx)
    - Security  (platform/reference/security.mdx)
Eval Mode/   (tab, icon: target)
  The eval loop/
    - Eval Mode  (eval-mode/index.mdx)
    - How eval mode works  (eval-mode/how-it-works.mdx)
    - Point OpenBat at your chatbot  (eval-mode/setup.mdx)
    - Probe with test queries  (eval-mode/probe.mdx)
    - Eval suites & regression diffs  (eval-mode/eval-suites.mdx)
    - Diagnose and fix  (eval-mode/diagnose-and-fix.mdx)
    - Test candidate prompts & backtests  (eval-mode/candidate-prompts.mdx)
    - Symptom-to-lever reference  (eval-mode/symptom-to-lever.mdx)
SDK/   (tab, icon: code)
  @openbat/sdk/
    - OpenBat SDK  (sdk/index.mdx)
    - SDK quickstart  (sdk/quickstart.mdx)
    - Configuration  (sdk/configuration.mdx)
    - Vercel AI SDK  (sdk/integrations/vercel-ai-sdk.mdx)
    - Node & Express  (sdk/integrations/node-express.mdx)
    - REST & other languages  (sdk/integrations/rest-http.mdx)
    - Enriching context  (sdk/enriching-context.mdx)
    - Header forwarding  (sdk/header-forwarding.mdx)
    - System prompt versioning  (sdk/system-prompt-versioning.mdx)
    - DB-backed system prompts  (sdk/db-backed-prompts.mdx)
    - Remote-controlled prompts  (sdk/remote-prompts.mdx)
    - Tool-aware verification  (sdk/tool-aware-verification.mdx)
    - Message deduplication  (sdk/deduplication.mdx)
    - API reference  (sdk/api-reference.mdx)
    - Limits & error handling  (sdk/limits-and-errors.mdx)
CLI/   (tab, icon: terminal)
  @openbat/cli/
    - OpenBat CLI  (cli/index.mdx)
    - Authentication & keys  (cli/authentication.mdx)
    - Pin the active chatbot  (cli/active-chatbot.mdx)
    - CLI quickstart  (cli/quickstart.mdx)
    - Command reference  (cli/commands.mdx)
    - Conversations & analytics  (cli/conversations-analytics.mdx)
    - Settings, keys & webhooks  (cli/settings-keys-webhooks.mdx)
    - Organizations & members  (cli/org-and-members.mdx)
    - Workflows & reports  (cli/workflows-reports.mdx)
    - Manage the live prompt  (cli/prompts.mdx)
    - Install the SDK from the CLI  (cli/sdk-install.mdx)
    - Security & rate limits  (cli/security-rate-limits.mdx)
MCP/   (tab, icon: plug)
  @openbat/mcp/
    - OpenBat MCP server  (mcp/index.mdx)
    - Install & configure  (mcp/install.mdx)
    - Credentials & authority  (mcp/credentials.mdx)
    - Pin to one chatbot  (mcp/pinning.mdx)
    - Tool reference  (mcp/tools.mdx)
    - Example configurations  (mcp/configs.mdx)
    - Security properties  (mcp/security.mdx)
    - Troubleshooting  (mcp/troubleshooting.mdx)
```

## Pages

### Get started

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `index` | Product overview — 'Google Analytics for AI chatbots'. | kb/onboarding-guide.md, kb/feature-inventory.md | 0 |
| `get-started/quickstart` | 5-minute path: create chatbot, install SDK, see data. | kb/onboarding-guide.md, sdk-readme.md, cli-readme.md | 1 |
| `get-started/how-openbat-works` | The capture -> analyze -> surface pipeline. | kb/architecture.md, kb/onboarding-guide.md | 0 |
| `get-started/concepts` | Glossary of the core entities and the auth-key ladder. | kb/architecture.md, kb/feature-inventory.md | 0 |
| `get-started/surfaces` | Orientation across the four product surfaces. | kb/onboarding-guide.md, cli-readme.md, mcp-readme.md, sdk-readme.md | 0 |

### Platform

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `platform/guides/sign-up-from-landing-page` | Task walkthrough: sign up from the landing page. | flows/sign-up-from-landing-page.md | 4 |
| `platform/guides/email-sign-up` | Task walkthrough: create your account. | flows/email-sign-up.md, pages/create-account.md | 5 |
| `platform/guides/email-login` | Task walkthrough: log in. | flows/email-login.md, pages/sign-in.md | 4 |
| `platform/guides/password-reset-request` | Task walkthrough: reset your password. | flows/password-reset-request.md, pages/forgot-password.md | 4 |
| `platform/guides/create-new-chatbot` | Task walkthrough: create a chatbot. | flows/create-new-chatbot.md, pages/chatbot-onboarding.md | 2 |
| `platform/guides/explore-demo-chatbot` | Task walkthrough: explore a demo chatbot. | flows/explore-demo-chatbot.md | 2 |
| `platform/guides/invite-team-member` | Task walkthrough: invite a team member. | flows/invite-team-member.md, pages/organization-members.md | 2 |
| `platform/guides/ask-ai-about-chatbot-data` | Task walkthrough: ask ai about your data. | flows/ask-ai-about-chatbot-data.md, pages/chatbot-overview-dashboard.md | 1 |
| `platform/guides/create-report-from-template` | Task walkthrough: create a report from a template. | flows/create-report-from-template.md, pages/reports.md | 2 |
| `platform/guides/create-workflow-from-template` | Task walkthrough: create a workflow from a template. | flows/create-workflow-from-template.md, pages/workflows.md | 3 |
| `platform/guides/create-new-prompt-version` | Task walkthrough: create a prompt version. | flows/create-new-prompt-version.md, pages/system-prompt.md | 2 |
| `platform/guides/review-a-specific-conversation` | Task walkthrough: review a conversation. | flows/review-a-specific-conversation.md, pages/conversation-detail.md | 2 |
| `platform/guides/configure-analysis-definitions` | Task walkthrough: configure analysis. | flows/configure-analysis-definitions.md, pages/analysis-config.md | 2 |
| `platform/guides/export-conversation-data` | Task walkthrough: export conversation data. | flows/export-conversation-data.md, pages/chatbot-settings.md | 2 |
| `platform/features/managing-chatbots` | Chatbot CRUD, status tabs, card/list views, org & user menus. | kb/feature-inventory.md, pages/chatbot-list-dashboard.md | 8 |
| `platform/features/overview-dashboard` | Metric cards, sparklines, risks, and the dashboard AI chat. | kb/feature-inventory.md, pages/chatbot-overview-dashboard.md | 4 |
| `platform/features/conversations` | Conversation list + full transcript/analysis detail view. | kb/feature-inventory.md, pages/conversations.md, pages/conversation-detail.md | 2 |
| `platform/features/deep-search` | Semantic conversation search. | kb/feature-inventory.md, pages/deep-search.md | 1 |
| `platform/features/query-types` | Semantic clustering of messages into canonical categories. | kb/feature-inventory.md, pages/query-types.md | 1 |
| `platform/features/users-and-organizations` | External user health/personas + customer-org directory. | kb/feature-inventory.md, pages/users.md, pages/external-customer-organizations.md | 2 |
| `platform/features/reports` | AI-native report/dashboard builder. | kb/feature-inventory.md, pages/reports.md | 1 |
| `platform/features/workflows` | Alert workflows, run history, and templates. | kb/feature-inventory.md, pages/workflows.md | 1 |
| `platform/features/system-prompt` | Prompt versioning, kill switch, rollback, experiments. | kb/feature-inventory.md, pages/system-prompt.md | 1 |
| `platform/features/analysis-config` | 7-tab analysis pipeline configuration. | kb/feature-inventory.md, pages/analysis-config.md | 1 |
| `platform/features/team-and-access` | Org/chatbot roles, invites, and org settings. | kb/feature-inventory.md, pages/organization-members.md, pages/organization-settings.md | 3 |
| `platform/features/chatbot-settings` | 7-tab chatbot settings panel. | kb/feature-inventory.md, pages/chatbot-settings.md | 1 |
| `platform/features/onboarding` | Guided SDK setup wizard. | kb/feature-inventory.md, pages/chatbot-onboarding.md | 1 |
| `platform/reference/architecture` | System architecture and the analysis pipeline. | kb/architecture.md | 0 |
| `platform/reference/page-map` | Full sitemap catalog (all 34 pages). | sitemap.json, sitemap.md | 0 |
| `platform/reference/security` | Encryption, data handling, access controls. | pages/security.md | 0 |

### Eval Mode

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `eval-mode/index` | Overview of the probe -> diagnose -> fix loop. | skill-openbat-eval.md, skill-openbat-optimize.md, cli-readme.md | 0 |
| `eval-mode/how-it-works` | Architecture + the MCP loop (openbat_probe/await/get); you drive the bot. | skill-openbat-eval.md, skill-openbat-optimize.md, mcp-readme.md | 0 |
| `eval-mode/setup` | openbat.probe.json adapter + active-chatbot scope. | skill-openbat-eval.md, cli-readme.md | 0 |
| `eval-mode/probe` | openbat probe + conversations await. | skill-openbat-eval.md, cli-readme.md | 0 |
| `eval-mode/eval-suites` | openbat eval run / eval diff. | skill-openbat-eval.md, cli-readme.md | 0 |
| `eval-mode/diagnose-and-fix` | openbat review/optimize -> symptom -> lever -> fix. | skill-openbat-optimize.md, cli-readme.md | 0 |
| `eval-mode/candidate-prompts` | create-draft, versionOverride, backtests. | skill-openbat-optimize.md, skill-openbat-eval.md, sdk-readme.md, cli-readme.md | 0 |
| `eval-mode/symptom-to-lever` | Reference table mapping signals to fixes. | skill-openbat-optimize.md | 0 |

### SDK

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `sdk/index` | SDK overview + install. | sdk-readme.md | 0 |
| `sdk/quickstart` | recordMessages quick start. | sdk-readme.md | 0 |
| `sdk/configuration` | OpenBatConfig + env vars. | sdk-readme.md | 0 |
| `sdk/integrations/vercel-ai-sdk` | Vercel AI SDK integration (README is authoritative for withOpenBat). | sdk-readme.md | 0 |
| `sdk/integrations/node-express` | Express/Node + the framework-agnostic Direct API pattern. | sdk-readme.md | 0 |
| `sdk/integrations/rest-http` | Raw HTTP / Python / curl capture. | sdk-readme.md | 0 |
| `sdk/enriching-context` | Context enrichment fields. | sdk-readme.md | 0 |
| `sdk/header-forwarding` | Forward x-original-* headers for real client metadata (any server integration). | sdk-readme.md | 0 |
| `sdk/system-prompt-versioning` | systemPromptTemplate/Variables versioning. | sdk-readme.md | 0 |
| `sdk/db-backed-prompts` | onPromptStateChange callback pattern. | sdk-readme.md | 0 |
| `sdk/remote-prompts` | getSystemPrompt runtime fetch. | sdk-readme.md | 0 |
| `sdk/tool-aware-verification` | Attaching tools/reasoning for hallucination checks. | sdk-readme.md | 0 |
| `sdk/deduplication` | message.id dedup semantics. | sdk-readme.md | 0 |
| `sdk/api-reference` | OpenBat class, withOpenBat, types, throws/auto-UUID/system-filter behavior. | sdk-readme.md | 0 |
| `sdk/limits-and-errors` | API limits, error handling, disabling. | sdk-readme.md | 0 |

### CLI

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `cli/index` | CLI overview + install. | cli-readme.md | 0 |
| `cli/authentication` | read/admin/pat/ingest keys + config set-key. | cli-readme.md, skill-using-openbat.md | 0 |
| `cli/active-chatbot` | openbat use / active-chatbot resolution. | cli-readme.md | 0 |
| `cli/quickstart` | End-to-end first-event quickstart. | cli-readme.md, skill-openbat-onboarding.md | 0 |
| `cli/commands` | Complete command tree. | cli-readme.md | 0 |
| `cli/conversations-analytics` | conversations, analytics, review, users, export. | cli-readme.md, skill-openbat-conversations.md | 0 |
| `cli/settings-keys-webhooks` | settings, keys, webhooks, and analysis-definition commands. | cli-readme.md, skill-openbat-settings.md | 0 |
| `cli/org-and-members` | org list/show/rename + members + invitations (PAT-only). | cli-readme.md, skill-using-openbat.md | 0 |
| `cli/workflows-reports` | workflows + reports commands. | cli-readme.md, skill-openbat-workflows.md | 0 |
| `cli/prompts` | prompts command group. | cli-readme.md | 0 |
| `cli/sdk-install` | sdk install-instructions / verify. | cli-readme.md, skill-openbat-sdk-install.md | 0 |
| `cli/security-rate-limits` | Security, base-URL override, audit log, rate limits. | cli-readme.md, skill-openbat-safe-mutations.md | 0 |

### MCP

| Page | Purpose | Sources | Images |
|---|---|---|---|
| `mcp/index` | MCP server overview. | mcp-readme.md | 0 |
| `mcp/install` | Get an API key + zero-install npx config per client. | mcp-readme.md | 0 |
| `mcp/credentials` | Credential detection + authority ranking. | mcp-readme.md | 0 |
| `mcp/pinning` | OPENBAT_CHATBOT_ID hard lock. | mcp-readme.md | 0 |
| `mcp/tools` | read/admin/pat tool tables. | mcp-readme.md | 0 |
| `mcp/configs` | Multi-kind config examples + OPENBAT_BASE_URL override. | mcp-readme.md | 0 |
| `mcp/security` | MCP security model. | mcp-readme.md | 0 |
| `mcp/troubleshooting` | Symptom/cause/fix table. | mcp-readme.md | 0 |

## Coverage

### Flows (14/14 mapped)
All discovered flows have a dedicated guide under **Platform > Guides**:

- Sign up from landing page
- Email login
- Email sign up
- Password reset request
- Create new chatbot
- Explore demo chatbot
- Invite team member
- Ask AI about chatbot data
- Create report from template
- Create workflow from template
- Create new prompt version
- Review a specific conversation
- Configure analysis definitions
- Export conversation data

### Product pages with a dedicated page
These sitemap pages are covered by a Guide, Feature, or Reference page:

- analysis-config
- chatbot-list-dashboard
- chatbot-onboarding
- chatbot-overview-dashboard
- chatbot-settings
- conversation-detail
- conversations
- create-account
- deep-search
- external-customer-organizations
- forgot-password
- organization-members
- organization-settings
- query-types
- reports
- security
- sign-in
- system-prompt
- users
- workflows

### Sitemap pages WITHOUT a dedicated page (intentional)
Marketing/collateral pages are catalogued in **Platform > Reference > Page map** but get no standalone doc page. Flagged here for your review:

- compare-overview
- compare-vs-braintrust
- compare-vs-diy
- compare-vs-helicone
- compare-vs-langfuse
- compare-vs-langsmith
- compare-vs-manual-review
- contact
- landing-page
- use-case-customer-success
- use-case-engineering
- use-case-product-teams
- use-case-support
- use-cases-overview

### Screenshots left unmapped (15)
Present in `scout-run/` but intentionally not wired (almost entirely marketing-page captures):

- screenshots/page-1.png
- screenshots/page-21.png
- screenshots/page-22.png
- screenshots/page-23.png
- screenshots/page-24.png
- screenshots/page-25.png
- screenshots/page-26.png
- screenshots/page-27.png
- screenshots/page-28.png
- state-screenshots/state-landing-accordion-hallucinations.png
- state-screenshots/state-landing-accordion-problem.png
- state-screenshots/state-landing-dropdown-compare.png
- state-screenshots/state-landing-dropdown-usecases.png
- state-screenshots/state-landing-faq.png
- state-screenshots/state-landing-tabs-sdk.png

### Notes / judgment calls
- **6 top-level tabs**, one per surface the user asked to keep separate: Get started, Platform, Eval Mode, SDK, CLI, MCP.
- **Eval Mode** is sourced from the `openbat-eval` + `openbat-optimize` agent skills (the probe -> diagnose -> fix loop), not from scout-run UI captures.
- **SDK/CLI/MCP** tabs are sourced from the published package READMEs, staged read-only under `_sources/` (mintignored) so the content phase has exact ground truth.
- Marketing pages (landing, use-cases, compare, contact) are intentionally **not** documented as product pages; they remain in the page-map catalog.
- Stray pre-existing file `docs/flows/password-reset.md` (a broken test stub, not in nav) — recommend deleting; left untouched by this pass (you have it open in the IDE).

### Content-phase notes (from the structure audit)
Guidance for the writers, surfaced by an adversarial review of this scaffold:

- **Source-of-truth conflict:** `_sources/skill-openbat-sdk-install.md` shows a stale 3-arg `withOpenBat(client, opts, factory)` form. The package README (`_sources/sdk-readme.md`) is authoritative — `withOpenBat(response, options)`. That skill was dropped from the SDK integration stubs' SOURCES.
- **Guide captions:** each guide `<Frame>` caption carries the ORIGINAL flow-step number (e.g. `flow step 2`) because scout captured non-contiguous steps; caption the right screen, not the file index.
- **Eval Mode division of labor:** `diagnose-and-fix` is the workflow and should LINK to `symptom-to-lever` for the canonical `answer_available x verification_source` table (don't duplicate it). Synthetic isolation (`kind=probe`, `--synthetic`, never claim prod metrics moved) belongs on `probe`/`how-it-works`. `backtests` commands come from `skill-openbat-optimize.md`, not the CLI README command tree.
- **Platform:** `overview-dashboard` content must document the dashboard AI-chat command hints (`@` tag, `$` plan, `#` user, `!` assistant, `^` prompt); auth-guide page images derive from `screenshots/page-2/3/4.png`.
- **Agent skills:** surface `npx skills add openbat-dev/agent-skills` on `cli/index` and `mcp/index` during the content pass — it's referenced across all three package READMEs.
