---
name: mermaid-diagrams
description: Use when preparing Mermaid diagrams for architecture, states, conditional logic, interactions, or customer journeys that a human needs to review. Not for screenshots, UI prototypes, or simple facts clearer in prose.
metadata:
  version: "0.2.1"
---

# Mermaid diagrams

Each diagram answers one question at a readable size. Keep the editable `.mmd` source and the verified renders with the task, not in the skill folder.

## Choose the view

| Question | View |
| --- | --- |
| What connects, and where are the boundaries? | Flowchart with named subgraphs |
| Which states and transitions are possible? | State diagram |
| Who sends what, in what order? | Sequence diagram |
| Which conditions lead to which outcomes? | Flowchart, or a decision table if clearer |
| What does the customer do, including interruptions? | Unscored flowchart; native journey only with supplied scores |

Label conditions and meaningful transitions. For alternative diagrams, reuse node IDs for the same steps. Say briefly whether the diagram shows proposed or observed behavior, and what is uncertain. Skip captions that repeat the diagram. Never invent journey scores, and never treat a timeout as proof that work stopped.

## Appearance

Use [assets/light.json](assets/light.json) and [assets/dark.json](assets/dark.json). Both use 20px Geist or Arial text, quiet surfaces and neutral connectors. Subgraphs sit on the page background inside a thin border. Colour carries meaning: blue for `decision`, teal for `result`; other nodes stay neutral. Assign classes with `class NODE_ID decision` or `class NODE_ID result`. Sequence participants use blue surfaces. Keep colours in the theme files, not in `classDef` lines. Name each outcome in words; colour alone is not enough.

Use soft fills without decorative node outlines. Branch labels need an opaque background and space around them so connectors do not cross the text; check both themes. Around a diagram, avoid numbered sections, repeated metadata, divider lines, nested borders and collapsible blocks.

Default to solid links. Non-solid links must mark needed distinctions, including optional steps. Explain each meaning in edge labels. Otherwise, use captions or legends. Flowcharts use solid `-->` and dotted `-.->`. Keep sequence `-->>` replies and async `-)` and `--)` arrows. Never add dotted or dashed decoration.

## Review presentation

Render with a transparent background. Follow the page’s light or dark theme and its theme switch; do not add a separate theme menu. Keep each SVG at its native size: scale down only while labels stay readable, and never stretch it to fill a page or viewer. Split a dense diagram or let it scroll instead of shrinking its text.

When a larger view helps, make the diagram itself open it by tap, click or keyboard. The viewer has a meaningful title and a small close button; Escape closes it and returns focus. Keep focus visible. Do not add Expand, View source or Download source buttons; keep source files with the task, out of the reviewer’s way. Give the page a short title a person would use, set apart by clear typographic hierarchy, not an internal key or a generic report heading.

## Render and verify

Requires Mermaid CLI (`mmdc`) with Node.js and the browser it drives, or another renderer. Use what is already installed. The themes are tested with Mermaid CLI 11.16.0; record the version you used.

```sh
mmdc -i /path/to/diagram.mmd -o /path/to/diagram-light.svg -c /path/to/mermaid-diagrams/assets/light.json -b transparent
```

Render the dark version with `dark.json`. Include `accTitle` and `accDescr`, and give the image useful alt text where it is shown. Look at both themes at the intended desktop and tablet sizes for clipped text, overlaps, labels crossing connectors and weak contrast. Test any viewer by touch, click and keyboard. Keep the renderer version and the evidence with the task. A diagram that parses has not been checked visually; mark unrendered work as unverified. Markdown hosts such as GitHub ignore these themes, so use verified images when appearance matters.
