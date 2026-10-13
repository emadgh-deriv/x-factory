---
name: define-mvp
description: Use when the user wants to turn a product idea into an MVP before any design or build - "define the MVP", "cut the idea down", "what should v1 be", or a change request on an existing docs/mvp.md. Reads docs/idea.md, checks the real backend, and writes docs/mvp.md with the core flow, the data check, an ordered feature backlog and done-when checks, then stops for review. Not for mockups or implementation.
---

# Define the MVP

The MVP is the **smallest product that is fully usable on real data**: one core flow, end to
end, connected to the real backend. Everything else waits in an ordered backlog. Cutting hard
here is what lets every later feature land on something that already works.

Input: `docs/idea.md` (the user's whole idea, any shape). Output: `docs/mvp.md`, built from
[`assets/mvp.template.md`](assets/mvp.template.md). This skill writes only those docs.

## 1. Read the idea

Read `docs/idea.md` in full. If it is missing, recreate it from the template's
`docs/idea.md` sections (or ask the user to describe the idea) and stop until it is filled.

List every feature the idea mentions, explicit or implied, as one line each. Done when every
sentence of the idea maps to a feature or to context.

## 2. Find the core flow

Pick the one journey without which the product has no reason to exist. Test each candidate:
*if this were the only thing that worked, would a real user still use the app?* Write it as
numbered user steps, from opening the app to the moment the user got value.

Keep sign-in, settings, personalisation and polish out of the core flow unless the flow cannot
run without them. When two flows compete, choose one and record the other as the first
backlog item and as an open question.

## 3. Check the data for real

The MVP must run on the real backend, so prove the backend can feed the core flow:

1. Fetch the machine-readable contract (OpenAPI/Swagger JSON, GraphQL schema) for each source
   in the idea. Call the public read endpoints once to see real payloads. Stay on read-only
   routes and keep keys out of URLs and files.
2. Map each core-flow step to the endpoint and fields that supply it.
3. Note auth, rate limits, CORS and anything that needs a server-side proxy.

Done when every core-flow step has a source, or is listed as a gap in Open questions. A step
with no data source is a blocker, stated plainly.

## 4. Order the backlog

Every other feature from step 1 goes into the backlog, ordered by: what users miss first,
then what later features depend on, then size. One line each: the feature and why it waits.
Mark features that need data the backend lacks.

## 5. Write `docs/mvp.md`

Fill every section of the template. **Done when** checks are observable on the running app
with real data (for example "latest 20 headlines load from <API> within 3 s on 4G throttling"),
covering loading, empty, error and slow-network states.

## 6. Hand back and iterate

Report the core flow in one sentence, the data blockers, the top three backlog items and the
open questions. Then wait.

Each change request edits the same `docs/mvp.md`. When the user approves, set
`Status: Approved`. The next step is `/feature-mockup the MVP`, which designs the core flow.
