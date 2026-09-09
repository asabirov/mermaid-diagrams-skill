---
name: mermaid-diagrams
description: Use when preparing Mermaid diagrams for architecture, states, conditional logic, interactions, or customer journeys that a human needs to review. Not for screenshots, UI prototypes, or simple facts clearer in prose.
---

# Mermaid diagrams

Explain one question at a readable size. Keep editable `.mmd` source and verified renders in the task’s artifacts, outside the installed skill.

## Choose the view

| Question | View |
| --- | --- |
| What connects, and where are the boundaries? | Flowchart with named subgraphs |
| Which states and transitions are possible? | State diagram |
| Who sends what, in what order? | Sequence diagram |
| Which conditions lead to which outcomes? | Flowchart, or a decision table if clearer |
| What does the customer do, including interruptions? | Unscored flowchart; native journey only with supplied scores |

Label conditions and meaningful transitions. Keep decision IDs stable across alternatives. Explain proposed versus observed behavior and material uncertainty briefly; omit captions that merely repeat the diagram. Never invent journey scores or treat a timeout as proof that work stopped.

## Appearance

Use [assets/light.json](assets/light.json) and [assets/dark.json](assets/dark.json). They share 16px Geist/Arial typography, quiet surfaces and neutral connectors. Colour has a semantic role: blue `decision`, teal `result`; ordinary nodes stay neutral. Assign classes with `class NODE_ID decision` or `class NODE_ID result`. Sequence participants use blue surfaces. Keep colours in the theme files, not repeated `classDef` values. Name outcomes explicitly; colour alone is insufficient.

Use soft fills without decorative node outlines. Keep branch labels off connectors with an opaque background and breathing room; inspect both themes. Avoid numbered sections, redundant metadata, divider lines, nested borders and disclosure blocks around diagrams.

## Review presentation

Render transparently. Match the page’s system light/dark theme and its visible theme switch; do not introduce a select menu. Preserve each SVG’s native dimensions: scale down only while labels remain readable, never stretch to fill a page or viewer. Split dense diagrams or allow local scrolling instead of shrinking their text.

When a larger view helps, make the diagram itself tappable and keyboard operable. Use a meaningful viewer title, a compact close button, Escape to close and return focus. Keep focus visible. Do not add Expand diagram, View source or Download source controls; retain source files in artifacts without exposing implementation controls in the review. Give the artifact a concise human title with clear typographic hierarchy, not an internal key or generic report heading.

## Render and verify

External dependency: Mermaid CLI (`mmdc`), Node.js and its working browser, or an equivalent renderer. Use existing tooling; [README.md](README.md) contains fixture commands and compatibility evidence.

```sh
mmdc -i /path/to/diagram.mmd -o /path/to/diagram-light.svg -c /path/to/mermaid-diagrams/assets/light.json -b transparent
```

Render the dark variant with `dark.json`. Include `accTitle` and `accDescr`; provide meaningful image alt text in the host. Inspect both themes at the intended desktop and iPad sizes for clipping, collisions, branch-label gaps and contrast. Test any viewer by touch/click and keyboard. Retain renderer version and evidence with the task. Source parsing alone is not visual verification; mark unrendered work unverified. Markdown hosts may ignore these themes: use verified images when appearance matters.
