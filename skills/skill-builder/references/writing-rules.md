# Writing Rules

## Include

| Include | Why |
|--------|-----|
| Non-obvious tool sequences | Agent would guess wrong |
| File format quirks | Not in training data or environment-specific |
| Output structure templates | Removes ambiguity |
| Target platform and folder path | Codex, Claude, and Copilot load skills from different places |
| Gotchas from known failure modes | Cheaper than letting the agent fail |
| Environment-specific paths or constraints | Not inferable |
| Examples when I/O format is ambiguous | One example beats three paragraphs |

## Omit

| Omit | Why |
|------|-----|
| How to write code | Agent knows |
| How to read files | Agent knows |
| General best practices the agent already follows | Noise |
| Motivation for instructions | Not instruction |
| Restatements of the description | Already in context |
| Steps for contextual decisions (naming, ordering) | Agent decides fine on its own |
| Reassurances ("this is important", "make sure") | Not instruction |

---

## Voice

Use imperative, second-person implied:

```txt
Good: Extract the filename from the path.
Good: Write assertions before running tests.
Bad: You should extract the filename from the path.
Bad: It's important to write assertions before running tests.
Bad: Feel free to extract the filename if needed.
```

---

## Gotcha list format

Use when: the agent might skip something, do something non-obviously wrong, or needs a constraint that doesn't fit in a process step.

Use grouped gotchas when there are multiple domains of failure:

```markdown
## Gotcha list

**Naming:**
- Use lowercase kebab-case for the skill folder and `name` field.
- Do not add prefixes unless the user requests one or the project already uses one.

**Packaging:**
- Package only from the skill folder, not from the repository root.
- Do not include generated cache or install artifacts in the package.
```

Use a flat list only when there are three or fewer gotchas:

```markdown
## Gotcha list
- Don't X when Y - agents commonly do this and it breaks Z.
- If condition A, do B instead of C.
- Output must be X format, not Y - the downstream tool requires it.
```

Gotchas are one line unless the context genuinely requires more.

---

## Naming format

Use lowercase kebab-case for every new skill folder and skill `name` field.

Examples:
- `implement`
- `review`
- `refactor`

Convert user-provided names to lowercase kebab-case.

Do not add prefixes unless the user explicitly requests one or the existing project convention requires one.

---

## Target platform format

Every new skill request must resolve these before writing files:
- Target platform: `codex`, `claude`, or `copilot`
- Scope: personal/global, project-local, or upload package
- OS/path style when the output is personal/global
- Output path and required main file name

Use `references/platform-targets.md` for the path matrix.

Do not assume a platform from the word "skill" alone. Ask one concise question when the target is missing.

Do not duplicate personal/global paths in the skill body unless necessary. Link to `references/platform-targets.md` so Windows, Unix, and WSL path forms stay centralized.

When writing Windows instructions, use `$env:USERPROFILE` for PowerShell and `%USERPROFILE%` for cmd. Do not write literal `~/.copilot` or `~/.codex` for Windows.

---

## When to write a process section vs a gotcha

**Write a process section** when there's a sequence of steps that must happen in order, involve non-trivial tool use, or have branching logic.

**Write a gotcha** when:
- The agent would do the right thing 80% of the time but fail in specific conditions
- The failure is non-obvious (the agent wouldn't realize it failed)
- The correct behavior is a single decision, not a sequence

---

## Description field formula

```txt
[What it does] + [output type] + [when to trigger] + [specific user phrases]
```

Optional: `[what it does NOT handle]` if there's a common near-miss.

Keep under 60 words. Test against:
1. A query that should trigger -> confirm it does
2. A near-miss query that shares keywords -> confirm it doesn't
