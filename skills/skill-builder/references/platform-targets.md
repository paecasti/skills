# Platform Targets

Use this compact reference to choose where a skill should be created.

## First decide

Resolve these before writing files:
1. Platform: `codex`, `claude`, or `copilot`
2. Scope: personal/global, project-local, CLI skill, or upload package
3. OS path style only when writing a personal/global path
4. Main file name: `SKILL.md` or `skill.md`

If the platform or scope is missing, ask one concise question. Do not ask about OS if the execution context exposes it.

## Home path notation

Use one home expression everywhere instead of repeating full paths per shell:

| Environment | Home |
|-------------|------|
| Windows PowerShell | `$env:USERPROFILE` |
| Windows cmd | `%USERPROFILE%` |
| Unix/macOS/Linux | `$HOME` |
| WSL | `$HOME` inside WSL |

Do not write literal `~/.copilot` or `~/.codex` for Windows instructions.

## File shape

Codex, Claude Code, and Copilot agent skills:

```txt
skill-name/SKILL.md
```

Claude.ai / Claude app upload skills:

```txt
skill-name/skill.md
```

Only add `resources/` folders when needed.

## Target matrix

| Target | Scope | Path template | Main file | Notes |
|--------|-------|---------------|-----------|-------|
| Codex | personal | `{CODEX_HOME}/skills/skill-name` or `{HOME}/.codex/skills/skill-name` | `SKILL.md` | Use `$env:CODEX_HOME` / `%CODEX_HOME%` / `$CODEX_HOME` when set. Restart Codex if the running session does not discover the new skill. |
| Codex | project | `.agents/skills/skill-name` | `SKILL.md` | Use only when repo-local behavior is requested. |
| Claude Code | project | `.claude/skills/skill-name` | `SKILL.md` | Folder name becomes the slash command, e.g. `/implement`. Prefer this over legacy `.claude/commands`. |
| Claude.ai / app | upload | `skill-name.zip` containing `skill-name/skill.md` | `skill.md` | ZIP the folder as the root entry, not just its files. |
| Copilot | project | `.github/skills/skill-name` | `SKILL.md` | Preferred repo-scoped Copilot skill path. |
| Copilot | project alternate | `.claude/skills/skill-name` or `.agents/skills/skill-name` | `SKILL.md` | Use only when requested or already standardized by the repo. |
| Copilot | personal | `{HOME}/.copilot/skills/skill-name` | `SKILL.md` | Use the OS-specific home expression above. Run `/skills reload` or start a new Copilot CLI session after adding it. |
| Copilot | personal alternate | `{HOME}/.agents/skills/skill-name` | `SKILL.md` | Shared agent-skill location. |

## Alias handling

Accept these aliases:
- `codex`, `codex-personal`, `codex-project`
- `claude`, `claude-code`, `claude-upload`
- `copilot`, `copilot-project`, `copilot-personal`

Infer `claude-code` when the user mentions a repository, CLI, slash command, or `.claude`.

Infer `claude-upload` when the user mentions Claude.ai, Claude app, Customize > Skills, upload, ZIP, Team, or Enterprise sharing.

## Copilot non-skill files

Only create these when the user asks for Copilot instructions or prompt files instead of an agent skill:

| Purpose | Path |
|---------|------|
| Repository instructions | `.github/copilot-instructions.md` |
| Path-specific instructions | `.github/instructions/NAME.instructions.md` |
| Reusable prompt | `.github/prompts/NAME.prompt.md` |

## Naming

Use lowercase kebab-case for the folder and skill `name`.

Examples:
- `implement`
- `review`
- `debug-ci`

Do not add prefixes unless the user explicitly requests one or the existing project convention requires one.
