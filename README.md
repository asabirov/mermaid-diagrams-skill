# Mermaid diagrams

An independent agent skill for readable architecture, states, conditional logic, interactions and customer journeys. It contains personal presentation preferences, light/dark themes and five rendering examples. It does not build review pages or depend on another skill.

Ask: “Show the customer’s review journey, including interruptions.” The agent chooses a diagram, renders both themes and checks the actual presentation. Rendering requires an available Mermaid renderer; these commands use [Mermaid CLI](https://github.com/mermaid-js/mermaid-cli), Node.js and its browser. No fonts are bundled: Geist is used when installed, otherwise Arial/sans-serif. Theme configuration follows [Mermaid’s documentation](https://mermaid.js.org/config/theming.html).

## Install and maintain

Clone into a skill directory named `mermaid-diagrams` in the agent’s supported skills location and check out a reviewed full commit SHA. Configuration repositories consume a pinned submodule at `skills/mermaid-diagrams`. Restart the agent, confirm discovery and request a sample render.

Record the old SHA before updating. Fetch the reviewed revision, verify a render and commit the changed configuration pin through a PR. Restore the old SHA to roll back; remove the clone or submodule to uninstall. Generated output belongs outside the package.

## Verify a change

The supplied configurations target Mermaid CLI 11.16.0. Recheck appearance when changing renderer versions; successful parsing does not establish visual compatibility. Run from the repository root:

```sh
mermaid_output=$(mktemp -d)
mmdc --version
for diagram in state sequence architecture logic journey; do
  for mode in light dark; do
    mmdc -i "checks/$diagram.mmd" -o "$mermaid_output/$diagram-$mode.svg" \
      -c "assets/$mode.json" -b transparent
  done
done
```

Fixtures cover review states, clipboard success/failure, delivery architecture, conditional visual selection and an interrupted customer journey. Render without per-source colour overrides or manual SVG patches. Inspect branch labels, class fills, connectors, accessibility titles/descriptions and text at desktop and iPad sizes against matching light/dark page backgrounds. The themes use opaque label backgrounds and a text halo to clear connectors. Presentation behavior belongs to the host: verify native dimensions, theme switching and keyboard/touch viewing there.

Compare the same review request against the prior skill: check view choice, editable sources, appearance, useful controls and honest verification limits. Include a nearby non-trigger such as a punctuation correction; it should not produce a diagram. Record inspected outputs, renderer version and limitations in the task’s GitHub record. These checks do not guarantee every host or model behaves identically.
