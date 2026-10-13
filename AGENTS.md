# Working in this repository

This project follows Base & Build: a working MVP first, then one feature at a time through an
approved mockup. Docs live in `docs/`: `idea.md`, `mvp.md`, `design-docs/mockups/`, `plans/`.

## Flow
1. `/define-mvp` turns `docs/idea.md` into `docs/mvp.md`. Approve before mocking up.
2. `/feature-mockup <feature>` writes a `.md` + `.html` mockup. Iterate on those files until approved.
3. `/build-from-mockup <feature>` builds one approved mockup and verifies it.

## Stack
- Language / framework:
- Design system:
- Backend / APIs:

## Scripts (run from the repo root)
- Dev:
- Build:
- Test:
- Lint / typecheck:

## Rules
- One feature per build request. Design changes go into the mockup first.
- Secrets live in `.env.local` (git-ignored) and in memory, never in tracked files, URLs or logs.
- Commit or push only when the user asks.
- Paste the literal output of the checks before reporting a task complete.
