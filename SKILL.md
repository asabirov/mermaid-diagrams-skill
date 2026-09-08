---
name: mermaid-diagrams
description: Use when preparing Mermaid diagrams for architecture, states, conditional logic, or interactions that a human needs to review. Not for screenshots, UI prototypes, or simple facts clearer in prose.
---

# Mermaid diagrams

Make the decision readable at the size the reviewer will see. Deliver editable `.mmd` source, a rendered SVG or PNG, and a short explanation of what the diagram establishes and what remains uncertain.

## Choose the view

| Question | View |
| --- | --- |
| What connects, and where are the boundaries? | `flowchart` with named subgraphs |
| Which states and transitions are possible? | `stateDiagram-v2` |
| Who sends what, in what order? | `sequenceDiagram` |
| Which conditions lead to which outcomes? | `flowchart`, or a decision table if clearer |

Use one question per diagram. Label relevant conditions, messages, and data movement. Separate an overview from details instead of shrinking a dense graph. Distinguish proposed behavior from observed behavior in the caption. Preserve decision IDs when comparing alternatives.

## Shared style

Load [assets/theme.json](assets/theme.json) when rendering. It defines Arial with sans-serif fallback, 16px text, white/gray surfaces, dark text and lines, and one blue accent. These are proposed defaults, not evidence of an approved personal preference.

Keep ordinary elements neutral. Reserve blue for the subject under discussion, using an explicit label as well as color. For a flowchart or state node, use:

```mermaid
classDef focus fill:#eff6ff,stroke:#2563eb,color:#172033
```

Apply `class NODE_ID focus` only where the renderer supports it. In sequence diagrams, use labeled notes or blocks to identify focus. Success, failure, and uncertainty must be named; color alone carries no meaning. Include `accTitle` and `accDescr`, plus a readable caption alongside the image.

## Render and inspect

External dependency: an available Mermaid renderer supporting the selected syntax and configuration; Mermaid CLI (`mmdc`) also requires Node.js and a working browser. Use its existing installation or declared project tooling. Resolve the skill path before running this example:

```sh
mmdc -i /path/to/diagram.mmd -o /path/to/diagram.svg -c /path/to/mermaid-diagrams/assets/theme.json -b white
```

Keep generated files and caches outside the installed skill. Inspect the actual rendered image for clipped labels, confusing crossings, contrast, and readable text at its intended display size; fix and rerender. Retain the source and report the renderer version with verification evidence. If rendering is unavailable, deliver source explicitly marked unverified.

Hosts may ignore custom themes in Markdown fences. Use the verified image when appearance matters and provide a usable link to both image and source. A source parse alone is not visual verification.
