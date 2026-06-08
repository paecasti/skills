---
name: skill-builder
description: Create, edit, or improve Codex, Claude, or Copilot skills. Use only when explicitly invoked as $skill-builder or when the user asks to create, edit, improve, or update an agent skill.
---

# Skill Builder

## What this skill produces

A target-specific skill package or folder for Codex, Claude, or Copilot.

---

## Core rules

Every line must change what the agent does. If removing a line does not change behavior, remove it.

Resolve the target before writing files:
- Platform: `codex`, `claude`, or `copilot`
- Variant: personal/global, project-local, CLI skill, or upload package
- OS/path style: Windows PowerShell, Windows cmd, Unix/macOS/Linux, or WSL

If the target platform is missing, ask one concise question before creating files.

Read `references/platform-targets.md` before choosing paths or filenames. Do not guess platform directories from memory.

Read `references/writing-rules.md` when drafting or editing the skill text.

---

## Naming

Use lowercase kebab-case for skill folders and skill `name` fields.

Examples:
- `implement`
- `review`
- `debug-ci`

Convert the user's requested name to lowercase kebab-case.

---

## Draft structure

Write the target skill as a thin validation gate plus deferred body:
- `SKILL.md` frontmatter: `name` and `description`
- `SKILL.md` title
- `SKILL.md` validation process: required checks that must pass before running the main process, so the agent does not execute unvalidated processes
- `SKILL.md` final validation step: if validation passes, read `references/body.md` and follow it
- `references/body.md`: What this produces, process, gotcha list, and examples only when input/output format is ambiguous

Keep `SKILL.md` small enough to validate without loading execution details. Put execution details in `references/body.md` so the agent reads them only after validation passes.

---

## Gotcha list

**Target:**
- Do not create files until the target platform and scope are known.
- Do not write literal Unix home shortcuts like `~/.copilot` for Windows PowerShell; use the Windows path form from `references/platform-targets.md`.
- Do not use `skill.md` for Codex, Claude Code, or Copilot agent skills; use `SKILL.md`.
- Do not use `SKILL.md` for Claude.ai upload packages; use lowercase `skill.md`.

**Naming:**
- Keep folder name and YAML `name` identical unless the target platform explicitly forbids it.
- Do not add prefixes unless the user explicitly requests one or the existing project convention requires one.

**Writing:**
- Do not explain why an instruction is good. Give the instruction.
- Do not pad descriptions to trigger more often. It causes false positives.
- Replace `feel free to`, `you might want to`, and `consider` with direct instruction or nothing.

---

## Output

Deliver output according to `references/platform-targets.md`.

For draft-only requests, present the main file content and the exact target path where it should live for the selected platform and OS.
