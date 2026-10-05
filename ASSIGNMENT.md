# MyNoteBook: Project Specification

## Product and timebox

Build a small SaaS where each user maintains **private personal notes and a personal ledger**. MyNoteBook offers Free and Pro plans and a sandbox upgrade flow. An administrator manages accounts, access, and subscription metadata.

Complete the project in **3–4 days**. Choose your stack and set it up yourself; no starter application is provided. A modern web frontend, a server/API, and **PostgreSQL with Prisma or Drizzle** are preferred. Alternatives are acceptable if explained and they meet the same persistence and security requirements. Managed database/auth services are acceptable; browser storage alone is not.

## Required behavior

### 1. Authentication, roles, and administration

- Support authenticated **ADMIN** and **USER** roles. Provide a safe, documented way to bootstrap a demo administrator; public registration must never grant ADMIN access.
- An admin can **create or invite users**, list accounts, **activate/suspend** users, assign **Free/Pro** plans, and view subscription status. Either creation or invitation is enough; an external email service is unnecessary.
- Created users must have a secure way to establish credentials. Invitations, if used, must expire and be single-use. Do not expose permanent passwords in API responses or commit demo credentials.
- Suspended accounts cannot access protected APIs, including through an existing session. Check current account status on the backend.
- Users can view their current plan, entitlements, and subscription status.
- **ADMIN does not automatically gain access to users' private notes or ledger entries.** Administrative screens and APIs expose account/subscription metadata only. Content remains owner-scoped even when the caller is ADMIN. Do not build impersonation or private-content browsing.

### 2. Private notes

- Create, list, view, update, and delete notes with a title, body, and timestamps.
- Support basic formatting, such as Markdown or a simple rich-text toolbar. Safely render formatted content; a complex editor is unnecessary.
- Add/remove tags and filter notes by tag. Tags belong to the current user.
- Handle empty lists, validation errors, and delete confirmation clearly.

### 3. Personal ledger

- Create, list, update, and delete entries with **INCOME or EXPENSE**, a positive amount, date, category, payment method, and description.
- Use a single documented currency. Use decimal or integer minor-unit storage/calculation to avoid floating-point money errors. Currency conversion is unnecessary.
- Categories and payment methods can be fixed lists or user-managed; document the choice.
- Show total income, total expenses, and net balance (**income minus expenses**). Include totals for the current filtered set and label them clearly; optional all-time totals must be labeled separately.
- Filter by date range, type, category, and payment method. Define date boundaries and timezone behavior consistently.

### 4. Search

- Provide case-insensitive search across note titles/bodies, tags, and ledger descriptions. Separate notes and ledger search inputs are acceptable.
- Combine search with relevant filters and provide a useful no-results state.
- Scope searches and aggregates to the authenticated owner. Never leak another user's tags, descriptions, counts, or totals.
- Database substring search is enough; a separate search engine is unnecessary.

### 5. Persistence and save feedback

- Persist accounts, notes, tags, ledger entries, plans/subscriptions, and payment history in a server-side database. Include a schema and reproducible migrations or equivalent setup.
- Notes and ledger edits display **Saving**, **Synced**, or **Failed** states. An explicit Save button or debounced autosave is acceptable.
- Show Synced only after the server confirms persistence. On failure, preserve unsaved input and offer retry; do not silently discard changes or report success.
- Saved data survives page reloads and a fresh login. Handle loading and API failures sensibly. If using autosave, prevent stale responses from overwriting newer edits.
- Online persistence is sufficient; offline synchronization is not required.

### 6. Free and Pro plans

- Display both plans and at least one meaningful difference, such as a Free note-count limit with a higher Pro limit, or a Pro-only ledger export.
- **Enforce at least one entitlement on the backend.** Hiding a button is insufficient. Direct API calls must not bypass limits or restrictions; account for concurrent requests where relevant.
- Define the chosen limits/features in your README and provide actionable upgrade feedback.
- Document downgrade behavior. Retain existing private data; if it exceeds the new limit, block additional creation rather than deleting records automatically.
- Keep plan entitlement and subscription/payment status distinct. Identify admin-assigned Pro as a manual assignment, not a fabricated successful payment. Define how manual assignments interact with subsequent verified payment events.

### 7. Sandbox payments and payment history

- Use a provider's **test/sandbox mode** for one Free-to-Pro purchase. A one-time sandbox purchase granting Pro is enough; automated recurring billing is not required.
- Initiate checkout from the backend and bind the payment to the authenticated user, intended plan, expected amount, and currency. Do not trust client-supplied prices or user IDs.
- Confirm success using a **signature-verified webhook or authenticated server-to-provider API verification**. A browser redirect, query parameter, or client-only success screen must never grant Pro.
- Verify payment/order identity, successful status, amount, currency, and user association before changing entitlement. Process repeated events idempotently to prevent duplicate history or upgrades.
- Store and show each user's payment history with provider reference, amount, currency, status, and timestamp. Handle pending, successful, and failed/cancelled outcomes without incorrectly upgrading the account.
- Show subscription/access status to users and admins; document the status model and whether Pro expires. Keep payment credentials and verification on the server.
- Include reproducible sandbox setup and verification instructions, including local webhook forwarding if used. Test fixtures support automated tests but do not replace the working sandbox integration.

### 8. Security and validation

- Use a proven authentication library/service or secure password hashing and session handling. Protect sessions for your architecture; document relevant cookie, CSRF, and token choices.
- Enforce authentication, roles, current account status, and **record ownership on every backend operation**, including reads, writes, search, aggregates, exports, tags, and payment history. Never rely on client checks or a supplied owner ID.
- Validate input on the backend: required fields, lengths, allowed types/statuses, valid dates, positive amounts, and safe formatting. Return clear errors without leaking secrets or internal stack traces.
- Keep database/payment credentials server-side; never expose them through public frontend environment variables. Do not store card data.
- Use synthetic data and keep secrets out of the repository, logs, screenshots, and demo instructions. Environment templates contain variable names and safe placeholders only.

### 9. Meaningful tests and documentation

Include automated tests for important behavior and regressions. Prefer realistic tests over shallow snapshots. Cover:

- Cross-user note/ledger access denied, including ADMIN trying to read another user's private content.
- Suspended-user access denied and non-admin account/plan-management access denied.
- Notes/ledger persistence and validation, plus representative filtered totals or search behavior.
- Backend entitlement rejection and successful Pro access.
- Verified payment success, rejected invalid/mismatched verification, and duplicate-event idempotency.

For save-state failure/retry, include an automated UI test or reproducible manual check. Document test commands, coverage, and known gaps. Mock provider boundaries in tests where appropriate, and separately demonstrate a real sandbox payment flow.

Your fork's README must explain prerequisites, installation, environment variables, database setup/migrations, synthetic demo data/account creation, local run commands, tests, architecture/schema, plan rules, sandbox verification, deployment if provided, and tradeoffs/limitations. State tools/libraries used and material AI assistance. Do not publish working credentials; provide local account-generation instructions or share necessary demo access privately through the original submission channel.

## Acceptance walkthrough

1. Start from a clean checkout and follow the README to launch the app and database.
2. Create an administrator and two users with synthetic data. Manage status and plans through admin tools.
3. As User A, create/edit/tag/search notes and create/filter/search ledger entries; verify totals and reload persistence.
4. Force a save failure, confirm Failed and preserved input, retry, and confirm Synced.
5. As User B and ADMIN, try fetching User A's private records through the API; access must be denied. Suspend User A and verify an existing session loses protected access.
6. Reach the Free entitlement boundary and try bypassing it with a direct API request; the backend must reject it.
7. Complete a sandbox payment; verify history and Pro entitlement. Repeat verification and test invalid/mismatched events; neither should cause an improper upgrade or duplicate history.
8. Run the documented tests and review limitations.

## Explicitly out of scope

Do not spend this timebox on graph features/graph visualization, CRDTs, realtime collaboration, complex offline sync, AI features, a mobile app, a complex block editor, production payments, or pixel-perfect UI. Also unnecessary: multi-currency accounting, bank integrations, enterprise analytics, and a full recurring-billing lifecycle. A readable, usable interface with clear feedback is sufficient.

## Suggested Day 1–4 plan

| Day | Focus | Target outcome |
| --- | --- | --- |
| 1 | Setup, schema/migrations, auth, ownership/roles, administration | App runs; two users have isolated access; admin manages accounts |
| 2 | Notes/tags, ledger, search/filters/totals, persistence/save states | Complete database-backed core user flows |
| 3 | Free/Pro entitlement, sandbox verification/history, security tests | Test-mode upgrade works; bypasses and invalid events are rejected |
| 4 | Finish tests, failure/retry checks, usability fixes, README, optional deployment | Reproducible submission with honest limitations |

For a three-day build, incorporate Day 4 verification/documentation into each day and keep the interface simple. Record actual time spent; do not add features to compensate for unfinished core requirements.

## Evaluation rubric — 100 points

| Area | Points | Evidence assessed |
| --- | ---: | --- |
| Authentication, authorization, privacy, admin controls | 25 | Secure sessions; ownership across APIs; admin privacy boundary; suspension; account/plan management |
| Notes, ledger, and search | 25 | Complete CRUD; formatting/tags; correct monetary totals; useful filters and owner-scoped search |
| Persistence and reliability | 15 | Reproducible database setup; reload persistence; truthful save states; preserved input/retry; sound data model |
| Plans and sandbox payments | 15 | Backend entitlement; verified upgrade; status model; idempotency; history/failure handling |
| Meaningful tests | 10 | Runnable boundary/critical-flow tests; relevant assertions; documented gaps |
| Documentation, maintainability, usability | 10 | Clean-checkout setup; clear architecture/tradeoffs; readable code; useful feedback; regular commits |
| **Total** | **100** | |

Full credit in each area means required flows work and evidence is reproducible; partial credit reflects working subsets or documented gaps; missing/nonfunctional behavior earns no credit for that portion. Unauthorized access, admin leakage of private content, exposed secrets, or client-trusted payment upgrades are critical defects that must be fixed before the project is complete. Extra features do not offset missing core behavior. An optional live demo is helpful but is not required for full credit.
