# MyNoteBook — Full Stack Developer Internship Project

Build **MyNoteBook**, a personal note-taking and personal ledger SaaS, in **3–4 days**. Users keep private notes, track income and expenses, and upgrade from Free to Pro through a sandbox payment flow. Administrators manage accounts and plans while respecting users' private content.

This repository contains the specification only. **There is no starter application code:** choosing and setting up the application, database, and project structure is part of the exercise.

## Get started

1. **Fork this public repository into your own GitHub account.**
2. Clone your fork and build MyNoteBook there, committing regularly.
3. Read [ASSIGNMENT.md](ASSIGNMENT.md) for requirements, the suggested Day 1–4 plan, and the evaluation rubric.
4. Replace or extend this README in your fork with setup, testing, and implementation documentation.
5. Follow [SUBMISSION.md](SUBMISSION.md) and submit **your fork URL**, plus an **optional live demo URL**, through the channel where you received the project.

**Do not open a pull request back to this repository.** Organization membership or collaborator access is unnecessary.

## Scope at a glance

- ADMIN and USER roles, account status, and plan management.
- Private notes with CRUD, basic formatting, and tags.
- A personal INCOME/EXPENSE ledger with categories, payment methods, totals, and filters.
- Search, server/database persistence, and Saving / Synced / Failed feedback.
- Free/Pro plans with a backend-enforced entitlement, verified sandbox payments, and payment history.
- Secure authentication, ownership authorization, validation, and meaningful tests.

PostgreSQL with Prisma or Drizzle is preferred. Choose a practical frontend/backend stack you can explain. Prioritize reliable core flows over extra features.

## Working guidelines

- Use synthetic demo data and test-mode payment credentials only. Never commit real secrets, private data, or production payment credentials.
- Copy [.env.example](.env.example) to a local environment file and adapt its names to your stack. The example contains no working credentials.
- Libraries and AI tools are allowed; document material assistance and understand your implementation.
- Stay within 3–4 days. Record time spent, tradeoffs, and unfinished requirements honestly.
- Graph features, CRDTs, realtime collaboration, complex offline sync, AI features, mobile apps, complex block editors, production payments, and pixel-perfect UI are out of scope.

## Repository contents

| File | Purpose |
| --- | --- |
| [ASSIGNMENT.md](ASSIGNMENT.md) | Requirements, acceptance checks, schedule, and rubric |
| [SUBMISSION.md](SUBMISSION.md) | Deliverables and submission template |
| [.env.example](.env.example) | Illustrative configuration with empty secret values |
| [.gitignore](.gitignore) | Common local, generated, and sensitive files to exclude |
| [LICENSE](LICENSE) | Apache License 2.0 |

The challenge materials are licensed under Apache-2.0. Preserve the license and applicable attribution when reusing them.
