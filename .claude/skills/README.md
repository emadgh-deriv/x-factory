# Skills

Claude Code skills that run the Base & Build loop. They ship in this template's
`.claude/skills/`; to reuse them elsewhere, copy the skill folders into that project's
`.claude/skills/`.

| Skill | Step | What it does |
|---|---|---|
| [`define-mvp`](define-mvp/SKILL.md) | 2 | Reads `docs/idea.md`, checks the real backend, writes `docs/mvp.md`: core flow, data check, ordered backlog, done-when checks. |
| [`feature-mockup`](feature-mockup/SKILL.md) | 3–4 | Writes and iterates a `.md` + `.html` mockup (desktop, mobile portrait, mobile landscape) for the MVP or a feature. |
| [`build-from-mockup`](build-from-mockup/SKILL.md) | 3–4 | Builds one approved mockup, verifies it on real data at all three sizes, reports. |
