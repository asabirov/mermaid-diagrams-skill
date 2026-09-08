# Mermaid diagrams

A lean agent skill for readable architecture, state, logic, and sequence diagrams. It supplies a shared theme and a source-plus-image delivery contract. It does not depend on another skill.

Ask: “Show the job lifecycle and retry behavior for review.” The agent chooses the view, applies the theme, and inspects the rendered result. Rendering needs an available Mermaid renderer; the CLI example needs [Mermaid CLI](https://github.com/mermaid-js/mermaid-cli), Node.js, and its browser. No dependency installation or network access occurs from this package itself. Theme options follow [Mermaid's configuration](https://mermaid.js.org/config/theming.html).

## Install and maintain

Clone this repository into a skill directory named `mermaid-diagrams` in your agent's supported skills location, then check out a reviewed full commit SHA. For a configuration repository, add it as a submodule at `skills/mermaid-diagrams` and commit the reviewed pin through a PR. Restart the agent and confirm `mermaid-diagrams` is listed; request a sample render to verify tooling.

Before updating, record the installed SHA. Fetch and check out the new reviewed SHA, verify a sample render, and commit the changed submodule pin where applicable. Roll back by restoring the previous SHA. Remove the installation or submodule to uninstall. Generated output belongs in your task's artifact directory, outside this package.

## Verify a change

Run the synthetic fixtures from the repository root (outputs stay outside the package):

```sh
mermaid_output=$(mktemp -d)
for diagram in state sequence architecture; do
  mmdc -i "checks/$diagram.mmd" -o "$mermaid_output/$diagram.svg" -c assets/theme.json -b white
  mmdc -i "checks/$diagram.mmd" -o "$mermaid_output/$diagram.png" -c assets/theme.json -b white
done
```

The fixtures cover retry states, timeout sequence branches, and an architecture boundary with focused worker. Preserve `.mmd` source and inspect SVG or PNG for label clipping, crossings, consistent fonts, contrast, and readability at review size. Record renderer version and results in the GitHub issue or PR.

Compare an agent's response to the same diagram request with and without the skill: check diagram choice, shared appearance, editable source, rendered inspection, and honest verification limits. Also ask a nearby non-trigger, such as “Correct this sentence's punctuation”; it should not create a diagram. These are behavioral checks, not guarantees across every model or renderer.
