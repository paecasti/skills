---
name: ground-code-references
description: Build a compact, source-grounded code reference report from named files or an ambiguous implementation request. Use when another model needs exact paths, symbols, lines, callers, tests, configs, and docs before deeper work. Produce references only; never resolve contradictions, business logic, design, bugs, or implementation.
---

# Ground Code References

## Validation

Run these checks before reading source files:

1. Require a readable code workspace or repository.
2. Require at least one grounding target: paths or request text containing a searchable identifier, feature term, route, error fragment, or behavior name. Ambiguous request text is valid.
3. Confirm every explicitly named source path exists and is readable.
4. If the user requests a report file, require a writable parent directory and explicit overwrite authorization when the file already exists.
5. If any check fails, stop and report every failure; otherwise read `references/body.md` and follow it.
