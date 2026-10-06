# Changelog

## 0.2.1 — Unreleased

### Changed

- **Link styles.** The agent uses solid links by default and explains any non-solid link that marks a needed distinction.

### Fixed

- **Dark edge labels.** You see full letters and hidden connectors on #0a0a0a, and matching theme copies blend labels into other dark pages.

## 0.2.0 — 2026-10-04

### Changed

- **Subgraphs are readable.** Subgraphs sit on the page background inside a thin border in both themes, so the nodes inside them stay visible.

- **Examples about a fictional online shop.** The five check diagrams cover an order lifecycle, card payment, shop architecture, a refund decision and an item return.

- **Tested version stated in the skill.** The skill names Mermaid CLI 11.16.0 as the tested renderer instead of pointing to the README.

## 0.1.0 — 2026-09-29

Mermaid diagrams helps you get a readable diagram for architecture, states, conditional logic, interactions or a customer journey that a person needs to review.

### Added

- **View selection by question.** The skill picks a flowchart, state diagram, sequence diagram, decision table or unscored journey based on the question being answered, rather than defaulting to one diagram type. This keeps the diagram matched to what actually needs explaining.

- **Light and dark theme assets.** You get diagrams rendered with consistent typography, quiet surfaces and semantic colour roles for decisions and results, in both a light and a dark theme. This keeps diagrams readable and consistent instead of relying on default Mermaid styling.

- **Reviewable presentation rules.** The skill renders diagrams at their native size, matches the host page's light/dark theme, and, when a larger view helps, makes the diagram tappable and keyboard operable without exposing source or download controls. This keeps the reviewer's focus on the diagram itself.

- **Render-and-verify workflow.** The skill renders both themes with Mermaid's command-line renderer and inspects them, with five example diagrams to test against, before a diagram is shared. This catches clipping, collisions and contrast problems before a reviewer sees them.
