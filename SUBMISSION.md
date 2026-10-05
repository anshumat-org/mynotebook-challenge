# Submit Your MyNoteBook Project

Build for **3–4 days** in a fork of this public repository under **your own GitHub account**. Submit your **fork URL** through the channel where you received the project. A **live demo URL is optional**. **Do not open a pull request back to the upstream repository.**

## Required deliverables

- Your GitHub fork with the application, regular commits, schema/migrations, tests, and updated README. Keep it accessible for review; a public fork is simplest.
- A README enabling a clean-checkout setup: prerequisites, installation, environment variables, database setup, synthetic seed data, safe account creation, run/test commands, and sandbox payment configuration/verification.
- Architecture, ownership/privacy checks, Free/Pro rules, payment/status behavior, actual time spent, tradeoffs, and unfinished requirements.
- Test coverage and a short walkthrough of the required flows in [ASSIGNMENT.md](ASSIGNMENT.md).
- No real secrets or private data. Keep environment files untracked and maintain a safe `.env.example`. Use test-mode payments only.

Optional deployment, screenshots, or a brief video can help demonstrate the app. They do not replace working source or setup instructions. Do not publish reusable passwords or payment keys in the repository, recording, or README; share necessary demo access privately through the original submission channel.

## Before submitting

- [ ] A clean checkout runs using the documented steps and migrations.
- [ ] ADMIN/USER behavior works, including suspension and private-content isolation.
- [ ] Notes/tags and ledger CRUD, search, filters, totals, and reload persistence work.
- [ ] Saving / Synced / Failed states and retry can be demonstrated.
- [ ] At least one Free/Pro entitlement is enforced on the backend.
- [ ] Sandbox verification, history, invalid-event rejection, and duplicate handling work.
- [ ] Tests run; failures or gaps are reported.
- [ ] README includes decisions, actual time spent, and limitations.
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
