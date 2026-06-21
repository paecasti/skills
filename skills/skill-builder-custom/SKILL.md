---
name: skill-builder-custom
description: Create, edit, or improve local project skills under a skills folder. Use only when explicitly invoked as $skill-builder-custom or when the user asks to create, edit, improve, or update an agent skill.
---

# Skill Builder Custom

## Core rules

Read `references/local-target.md` before creating or moving skill files.

Read `references/writing-rules.md` before drafting or editing skill text.

Create and edit only project-local skills under `skills/`.

Use lowercase kebab-case for new skill folder names and `name` fields.

Keep each new `SKILL.md` as a validation gate. It must stop before reading references when validation fails, report the failed validations to the user, and read `references/body.md` only after all validations pass.

---

## Output

For draft-only requests, present the file content and target path without creating files.
