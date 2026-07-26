# Ground Code References Body

## Boundaries

- Treat code and source documentation as read-only.
- Do not diagnose bugs, validate correctness, explain business rules, resolve contradictions, make design decisions, recommend changes, or implement anything.
- Describe only syntactic or explicitly documented roles needed to identify a reference.
- Use the request language for the report and preserve identifiers verbatim.
- Return the report in the response unless the user explicitly requests a file.

## Search workflow

1. Record the supplied paths and request text without interpreting intent.
2. Build a small search vocabulary from literal identifiers, path fragments, route names, error text, and distinctive feature terms in the request.
3. Inventory likely files with `rg --files`, then search with `rg -n`. Ignore `.git`, `node_modules`, `vendor`, `dist`, `build`, `coverage`, `.next`, and `target` unless the user names them or source evidence points to them.
4. Read narrow surrounding regions instead of whole files when possible.
5. Follow only edges that can receive an evidence label defined below.
6. For an ambiguous request, keep distinct candidate clusters separate. State the literal match or reference edge that produced each cluster; do not select the intended cluster.
7. Expand at most two reference hops from each seed unless the user requests exhaustive coverage.
8. Stop when the seeds connect to their definitions and nearest consumers, tests, configuration, or documentation, or when another search pass yields no new direct references.
9. Prefer at most 25 high-value references. Remove duplicate import sites and low-signal text matches before omitting definitions, entry points, tests, or configuration.

## Evidence labels

- `definition`: declares the symbol or primary artifact.
- `entry`: registers or exposes an entry point.
- `import` or `re-export`: creates a module edge.
- `call` or `consumer`: directly uses the symbol.
- `implementation`: implements a discovered interface or contract.
- `test`: directly exercises the symbol, route, or term.
- `config`, `schema`, `migration`, or `template`: supplies an adjacent declarative artifact.
- `doc`: explicitly documents the symbol or term.
- `text-match`: contains only a lexical match; do not imply a stronger relationship.

Use `core` for direct seeds, definitions, and entry points; `linked` for first-order reference edges; and `context` for tests, configuration, schemas, templates, examples, and docs. These labels indicate reference distance, not importance to the business.

## Report format

```md
# Grounding references

## Search basis

- Request: <request text, lightly condensed without resolving it>
- Supplied paths: <repo-relative paths or None>
- Search terms: `<term>`, `<term>`
- Scope: <directories searched and default exclusions>

## Core references

- `path/to/file.ext:line` — `symbol-or-artifact` — [evidence-label] <one factual syntactic role>

## Linked references

- `path/to/file.ext:line` — `symbol-or-artifact` — [evidence-label] <direct relationship>

## Context references

- `path/to/file.ext:line` — `symbol-or-artifact` — [evidence-label] <direct relationship>

## Relationship map

- `source.ext:line` --<reference-edge>--> `target.ext:line`

## Candidate clusters

### <neutral cluster label>

- Basis: `<literal term or reference edge>`
- References: `path:line`, `path:line`

## Search gaps

- `<exact query>` — no match in `<searched scope>`

## Analysis boundary

Not analyzed: contradictions, business rules, correctness, architecture choices, fixes, or implementation.
```

Omit empty sections. Always include `Search basis` and `Analysis boundary`; include `Search gaps` when nothing matches.

## Quality checks

1. Give every source claim a verified current repository-relative path and 1-based line number.
2. Verify each evidence label against visible source; use `text-match` for lexical-only matches or inferred framework behavior.
3. Keep snippets out of the report unless a short literal is required to distinguish matches.
