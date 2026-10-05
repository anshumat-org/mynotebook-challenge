# Submit Your MyNoteBook Project

Build for **3–4 days** in a fork of this public repository under **your own GitHub account**. Submit your **fork URL** through the channel where you received the project. A **live demo URL is optional**. **Do not open a pull request back to the upstream repository.**

## Required deliverables

- Your GitHub fork with the application, regular commits, schema/migrations, tests, and updated README. Keep it accessible for review; a public fork is simplest.
- A README enabling a clean-checkout setup: prerequisites, installation, environment variables, database setup, synthetic seed data, safe account creation, run/test commands, and sandbox payment configuration/verification.
- Architecture, ownership/privacy checks, Free/Pro rules, payment/status behavior, actual time spent, tradeoffs, and unfinished requirements.
- **A system flow diagram and a product flow diagram are required.** Include both in your README or linked documentation inside your fork; follow the guidance below.
- Test coverage and a short walkthrough of the required flows in [ASSIGNMENT.md](ASSIGNMENT.md).
- No real secrets or private data. Keep environment files untracked and maintain a safe `.env.example`. Use test-mode payments only.

Optional deployment, screenshots, or a brief video can help demonstrate the app. They do not replace working source or setup instructions. Do not publish reusable passwords or payment keys in the repository, recording, or README; share necessary demo access privately through the original submission channel.

## Required flow diagrams

These diagrams are an important part of the submission. They should explain your actual implementation clearly and match the working application. Use Mermaid in Markdown, an exported image, or a PDF; keep each diagram readable and link it from your README. Documentation diagrams are required even though graph features inside the application remain out of scope.

### System flow diagram

Show how the system's components interact:

- Frontend, authentication/session handling, backend/API, and database.
- Where role, account-status, ownership, and Free/Pro entitlement checks happen.
- How note and ledger changes reach the database, and how success/failure responses drive Saving / Synced / Failed states.
- Sandbox checkout, payment provider, verified webhook or server-side API verification, payment history, and plan updates.
- The admin boundary: account/subscription management without access to another user's private notes or ledger.

Label the main requests, responses, and data transitions. Make clear which operations happen in the browser, on the server, in the database, and at the payment provider.

### Product flow diagram

Show the main user journeys and their important decisions:

- USER sign-in, notes creation/editing, formatting/tags, search, and save feedback/retry.
- Ledger entry creation/editing, search/filtering, and viewing totals.
- Reaching a Free-plan limit, choosing Pro, sandbox checkout, pending/success/failure outcomes, and viewing the resulting plan and payment history.
- ADMIN creating/inviting a user, activating/suspending an account, assigning a plan, and viewing subscription status.
- What a suspended user sees and what happens when an action is denied.

Use separate USER and ADMIN paths or clearly labeled sections. Include important failure/retry paths, not only the successful journey. Keep the diagrams concise; decorative or pixel-perfect diagram design is unnecessary.

## Before submitting

- [ ] A clean checkout runs using the documented steps and migrations.
- [ ] ADMIN/USER behavior works, including suspension and private-content isolation.
- [ ] Notes/tags and ledger CRUD, search, filters, totals, and reload persistence work.
- [ ] Saving / Synced / Failed states and retry can be demonstrated.
- [ ] At least one Free/Pro entitlement is enforced on the backend.
- [ ] Sandbox verification, history, invalid-event rejection, and duplicate handling work.
- [ ] Tests run; failures or gaps are reported.
- [ ] README includes decisions, actual time spent, and limitations.
- [ ] System flow and product flow diagrams are included, linked from the README, and match the implementation.
- [ ] No secrets, database dumps, private data, or production credentials are committed.
- [ ] The submitted URL points to your own fork, not the upstream repository.

## Submission template

Copy this into your message through the original submission channel. There is no submission API or email address configured in this repository.

```text
MyNoteBook submission

GitHub fork URL (required):
Commit SHA reviewed (recommended):
Live demo URL (optional):
Screenshots/video URL (optional):
System flow diagram path/link (required):
Product flow diagram path/link (required):

Time spent / days worked:
Stack and database:
Implemented core requirements:
Free/Pro entitlement and limits:
Sandbox payment provider and verification method:
Test command and result:
Known limitations / unfinished requirements:
Key tradeoffs:
Libraries/tools and material AI assistance:
Demo account setup: See README (share hosted access privately).
```
