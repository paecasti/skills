# Writing Rules

## Keep

- Non-obvious tool sequences, file format quirks, output templates, local path rules, failure gotchas, and examples only when input or output is ambiguous.
- `SKILL.md`: frontmatter, title, validation checks, failure reporting, and the final step to read `references/body.md` only after validation passes.
- `references/body.md`: production workflow, required artifacts, gotchas, and examples only when needed.
- Descriptions under 60 words, specific to the trigger phrases that should activate the skill.

## Remove

- Motivation, reassurance, restatements of the description, and generic writing advice.
- Instructions for coding, reading files, or choosing ordinary markdown structure.
- Prefix rules unless the user requests one or the project already uses one.
- Platform, personal/global, upload, CLI, or OS-path branching.
