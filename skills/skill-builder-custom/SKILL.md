---
name: skill-builder-custom
description: Create, edit, or improve agent skills. Use only when explicitly invoked as $skill-builder-custom or when the user asks to create, edit, improve, or update an agent skill.
---

# Skill Builder Custom

## Core rules

Read `references/writing-rules.md` before drafting or editing skill text.

Use lowercase kebab-case for new skill folder names and `name` fields.

Keep each new `SKILL.md` as a validation gate. It must stop before reading references when validation fails, report the failed validations to the user, and read `references/body.md` only after all validations pass.

---

## Output

For draft-only requests, present the file content and target path without creating files.
