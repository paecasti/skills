# HTML Explainer Body

## What this produces

A single standalone `index.html` file in `html-explainer/` next to the primary document.

## Process

1. Read the primary document first.
2. Read supporting documents only after the primary document.
3. Identify the source language and write the generated page in that language unless the user asks otherwise.
4. Extract the document purpose, audience, key facts, decisions, requirements, acceptance criteria, flow steps, risks, open questions, and source relationships when present.
5. Preserve source intent. Do not silently resolve conflicts, missing details, or unclear ownership; surface them in the generated page.
6. Create the `html-explainer/` directory if it does not exist.
7. Generate only `html-explainer/index.html`.
8. Put all CSS and JavaScript inline in that file.
9. Do not use external frameworks, package installs, CDNs, or build steps.
10. Do not edit the primary or supporting documents.

## Page requirements

1. Include a clear title based on the primary document.
2. Include an overview that explains what the source material specifies.
3. Include a source map that names the primary document and each supporting document.
4. Use structured sections that match the source material, such as goals, decisions, acceptance criteria, plan steps, workflow, risks, assumptions, or open questions.
5. Use visual treatments when they help understanding: timelines, flow blocks, checklist groups, compact cards, comparison tables, or inline SVG diagrams.
6. Keep the page readable without network access.
7. Keep interactions optional and lightweight, such as section filters, expand/collapse details, or small navigation helpers.

## Gotcha list

- Do not create CSS, JavaScript, image, or asset files outside `index.html`.
- Do not summarize away important constraints, caveats, or unresolved questions.
- Do not claim conflicts are resolved unless the sources explicitly resolve them.
- Do not overwrite an existing `index.html` unless validation confirmed overwrite authorization.
- Do not transform the source documentation itself.
