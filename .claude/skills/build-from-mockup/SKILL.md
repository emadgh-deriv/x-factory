---
name: build-from-mockup
description: Use when the user wants an approved mockup implemented - "build X from the mockup", "build the MVP", "implement the approved mockup". Reads the approved .md + .html pair, writes a short build plan, implements that one feature to match every frame and state, verifies it in the running app on real data, and reports. Not for designing or changing the design; that is feature-mockup.
---

# Build from mockup

The approved mockup pair is the **spec**: the `.md` says what and why, the `.html` shows
exactly how it looks in desktop, mobile portrait and mobile landscape. Build one feature,
exactly as specified, on top of the working product.

## 1. Check the gate

Find the pair in `docs/design-docs/mockups/`. Both files must say `Status: Approved`. If they
say anything else, stop and tell the user the mockup needs approval first.

Read in full: the mockup `.md`, the `.html` (open it in the browser and look at every frame),
`docs/design-docs/mockups/PROFILE.md`, `docs/mvp.md`, and the project's `AGENTS.md`.

## 2. Write the build plan

Write `docs/plans/YYYY-MM-DD-<feature>.md`:

- **Files**: each file to add or change, and why.
- **Order**: data layer, then state, then UI, then wiring into the shell.
- **Coverage**: every screen, every annotation number and every state from the mockup, each
  mapped to the file that delivers it.
- **Risks**: anything the mockup assumes that the code or the data does not support yet.
- **Proof**: the tests to write and the checks to run in the browser.

Done when every annotation and every state in the mockup has a line in Coverage.

If the plan shows the mockup cannot be built as drawn (missing data, a component that does
not exist, a conflict with the working product), stop and report it. The fix goes back into
the mockup through `/feature-mockup`, then the build resumes from the updated pair.

## 3. Build

Follow the plan's order. Use the components and tokens the mockup uses, from the project's
design system. Implement every state the mockup lists. Keep the change inside this feature:
the rest of the product keeps working, and a failure in this feature degrades only this
feature. Write tests first for logic and data parsing. Keep secrets in `.env.local` and in
memory.

When the build has to depart from the mockup, write the change and the reason into the plan
before the code lands.

## 4. Verify

1. Run the project's checks (build, lint, typecheck, tests) and paste the literal output.
   Fix the code when a test fails.
2. Run the app against the real backend and drive the feature end to end.
3. Screenshot the feature at desktop, mobile portrait (390×844) and mobile landscape
   (844×390) and compare each with its mockup frame. Trigger each state (loading, empty,
   error, slow network) and compare it too.
4. Re-run the MVP core flow from `docs/mvp.md` to confirm nothing it depends on broke.

Done when every Coverage line is checked off in the plan, each with how it was verified.

## 5. Report

Report what was built, the check output, the screenshots, every departure from the mockup and
anything you could not verify, said plainly. Set `Status: Built` in the mockup pair and the
mockups README row. Leave committing to the user unless they asked for it.
