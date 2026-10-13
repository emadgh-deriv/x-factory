---
name: feature-mockup
description: Use when the user wants a mockup, wireframe or design proposal for a new or changed feature (or the MVP) before it is built - "mock up X", "show me what X would look like", a feature request with a reference screenshot, or a change request on an existing mockup. Produces a paired Markdown + HTML mockup with desktop, mobile portrait and mobile landscape frames, grounded in the project's real layout, design system and data, then stops for review. Not for implementation.
---

# Feature mockup

A mockup is the **spec a builder can follow without asking questions**: one `.md` and one
`.html` with the same basename in the project's mockup folder. All design iteration happens on
these two files. You stop after writing them; building starts only when the user approves.

The project's facts (design system, app shell, breakpoints, data sources, copy rules) live in
the **profile**, `docs/design-docs/mockups/PROFILE.md`. It is the single source of truth for
every mockup in the repo. Read it first. If it does not exist, do step 0.

## 0. Create the profile (first run in a repo only)

Copy [`assets/PROFILE.template.md`](assets/PROFILE.template.md) to
`docs/design-docs/mockups/PROFILE.md` and fill every section from the repo: the component
library and token file, the app shell measurements from the real layout code, the breakpoints
in the CSS, the API contracts, and any copy or compliance rules in `AGENTS.md`.
Write "unknown" where the repo has no answer and ask the user only about those. Done when no
section is blank.

## 1. Understand before drawing

1. **Restate the intent** in two or three sentences: what the user does and what they see.
   For a reference screenshot, list what it shows element by element.
2. **Read the data for real.** Fetch the machine-readable contract (OpenAPI/Swagger JSON,
   GraphQL schema, protobuf), list the endpoints, parameters, enums and response shapes, and
   call the public read endpoints once to see real payloads. Stay on read-only routes and keep
   tokens out of URLs and files.
3. **Diff the reference against the data.** A table: *reference has / data has / mockup does*.
   Draw what the data supports and put each gap in Open questions. This table is the most
   valuable part of the document.
4. **Place it in the real shell** using the profile's layout and the earlier mockups in the
   folder. Reuse their measurements.

Ask the user only when the answer changes what you draw. Otherwise choose, mark it
"proposal" and list it under Open questions.

## 2. Write the Markdown: `YYYY-MM-DD-<feature>.md`

Sections, in order:

- Header: date, `Status: Proposed`, link to the HTML, data source and version.
- **Intent**.
- **Data reality**: the diff table, endpoints and parameters used, fields used, fields left
  out and why, and the exact rule for every derived value.
- **Screens**: table of # · screen · desktop · mobile portrait · mobile landscape.
- One subsection per screen: an ASCII wireframe, then an annotation table
  (`# | Element | Behaviour`). Numbers match the markers in the HTML.
- **States**: loading, empty, filtered-to-empty, error/service down, not applicable. Say how
  a failure of this feature leaves the rest of the product working.
- **Components used**: each one, and whether it exists in the library or is new.
- **Open questions**, numbered, each one a decision for the user.

Done when a builder could implement every screen and state from this file alone.

## 3. Build the HTML: same basename, `.html`

Every screen appears in **three frames**: desktop (profile width, default 1280×800), mobile
portrait (390×844) and mobile landscape (844×390). Start from
[`assets/mockup-frame.html`](assets/mockup-frame.html), which has the frames, annotation
markers and page layout.

Render controls from the **project's own design system** so the mockup shows the UI that will
ship:

- If the profile names a render command for real components, write the page as a component
  entry and render it with that command into one self-contained `.html`.
- Otherwise inline the design system's CSS and token file and use its class names and markup.
  Custom markup is for what the library has no component for (charts, frames, annotations) and
  uses tokens only.

Then:

- Annotation markers are numbered purple dots tied to the Markdown tables. Outline new
  elements with a dashed purple border so the proposal never reads as already built.
- Show a visible data caveat at the top when the reference promises more than the data gives.
- Use sample data shaped like the real payloads, labelled illustrative.
- When a render step exists, edit the source and rebuild; the `.html` is generated.

## 4. Verify

Open the HTML in the browser (serve the folder over HTTP if it is large). Check the console
is clean, then screenshot every frame. Fix overflow, overlapping controls and markers that
point at nothing. Confirm the design system's styles applied by reading the computed style of
one instance of each component. Done when every frame renders cleanly at its size.

Add a row for the mockup to `docs/design-docs/mockups/README.md`, status **proposed**.

## 5. Hand back and iterate

Report the two paths, the three to six findings that most affect the design (data gaps
first) and the open questions. Then wait.

Each change request edits **the same two files**: update the Markdown, rebuild or edit the
HTML, keep frames and annotation numbers in sync, re-verify, and summarise what changed. One
file pair per feature for its whole life.

When the user approves, set `Status: Approved` in both files and the README row. The approved
pair is the build spec.
