# mermaid-diagrams-skill

Readable Mermaid diagrams with a consistent visual style.

This is an agent skill. When someone has to review architecture, states,
conditional logic, an exchange of messages or a customer journey, the agent
picks the diagram type that fits the question. It renders the diagram in a
light and a dark theme, then checks the rendered images before showing them.

## Why it exists, and what it turned down

Left alone, an agent tends to draw a flowchart for everything, use Mermaid's
default styling and call a diagram done once it parses. This skill makes it
choose the view by the question, render with a shared theme and look at the
result.

What it turned down:

- **Default Mermaid styling.** Two theme files set the type, surfaces and two
  meaning-carrying colours, so diagrams look alike across tasks.
- **Colour defined inside each diagram.** Colours live in the theme files.
  Diagrams only name a class: `decision` or `result`.
- **Invented journey scores.** Mermaid's native journey chart needs a score
  for each step. The skill draws journeys as unscored flowcharts unless real
  scores are supplied.
- **Parsing as proof.** A diagram that parses can still clip text or hide a
  label under a connector. The skill counts only an inspected render as
  verified.
- **Review-page building.** The skill makes diagrams. It does not build the
  page they are reviewed on, and it does not depend on any other skill.

## The design

| Question | View |
| --- | --- |
| What connects, and where are the boundaries? | Flowchart with named subgraphs |
| Which states and transitions are possible? | State diagram |
| Who sends what, in what order? | Sequence diagram |
| Which conditions lead to which outcomes? | Flowchart, or a decision table if clearer |
| What does the customer do, including interruptions? | Unscored flowchart |

**Text is 20px.** The themes set 20px text so a diagram stays readable on a
tablet without zooming.

**Two colours, each with a meaning.** Blue marks a decision and teal marks a
result. Everything else stays neutral grey, and each outcome is also named in
words, so colour is never the only cue.

**Labels sit on an opaque background.** Branch labels get a solid background
and a halo in the page colour, so a connector never runs through the text.

**Themes need a real renderer.** Markdown hosts such as GitHub use their own
Mermaid theme and ignore these files. Where appearance matters, the skill
shares verified images.

## What's where

| Path | Owns |
| --- | --- |
| `SKILL.md` | The rules the agent follows: view choice, appearance, presentation, render and verify |
| `assets/light.json`, `assets/dark.json` | Mermaid CLI configuration for each theme |
| `checks/*.mmd` | Five example diagrams about a fictional online shop, one per view, used to check a theme or renderer change |
| `CHANGELOG.md` | What changed in each release |
| `.github/workflows/notify-private-repo.yml` | After a merge to `main`, tells the owner's private config repo to update its pinned copy. It needs a secret that forks do not have. |

## How to run and verify it

You need [Mermaid CLI](https://github.com/mermaid-js/mermaid-cli) and Node.js.
The themes are tested with Mermaid CLI 11.16.0. No fonts are bundled: Geist is
used when installed, otherwise Arial.

Render every example in both themes from the repository root:

```sh
mermaid_output=$(mktemp -d)
mmdc --version
for diagram in state sequence architecture logic journey; do
  for mode in light dark; do
    mmdc -q -i "checks/$diagram.mmd" -o "$mermaid_output/$diagram-$mode.svg" \
      -c "assets/$mode.json" -b transparent
  done
done
ls "$mermaid_output"
```

Output on 2026-10-03:

```text
11.16.0
architecture-dark.svg
architecture-light.svg
journey-dark.svg
journey-light.svg
logic-dark.svg
logic-light.svg
sequence-dark.svg
sequence-light.svg
state-dark.svg
state-light.svg
```

Ten files mean every example parsed and rendered. They do not prove the
diagrams look right. Open each one on a page of the matching background
colour. Check the branch labels, the blue and teal fills, the subgraph borders
and the text at desktop and tablet widths.

To install the skill for Claude Code, clone it into a folder named after the
skill, then start a new session:

```sh
git clone https://github.com/asabirov/mermaid-diagrams-skill ~/.claude/skills/mermaid-diagrams
```

Other agents that read `SKILL.md` folders work the same way. Ask for a diagram,
for example "Show the states an order goes through, including
refunds." The agent should choose a state diagram and render both themes.

To check a change to `SKILL.md`, give the same review request to the old and
the new version. Compare the view chosen, the source files kept, the
appearance and how honestly each states what it did not verify. Also send a
nearby request that should not produce a diagram, such as a punctuation fix.

The version is `metadata.version` in `SKILL.md`. Changes are listed in
[CHANGELOG.md](CHANGELOG.md).

## Licence

[MIT](LICENSE), © 2026 Artur Sabirov.
