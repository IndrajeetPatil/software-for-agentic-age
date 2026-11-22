# AGENTS.md

A single-page [Quarto](https://quarto.org/) presentation rendered to
[RevealJS](https://revealjs.com/) slides and deployed as a static site via
GitHub Pages.

## Checks

`just render` must succeed after every change; CI builds the deck on every
pull request.

## Key conventions

- **Single-file deck.** All slides live in `index.qmd`; do not split it.
- **Design specification.** The visual design follows [DESIGN.md](DESIGN.md).
  Respect it when creating or modifying slides, components, styling, colours,
  and typography. Colours and fonts live in `_brand.yml`,
  while `style.css` defines the neo-brutalist shapes (3px ink borders, hard
  offset shadows, and slightly tilted cards). Use the existing component
  classes (`.card`, `.grid-2|3|4`, `.callout-big`, `.tag`, `.sticker`, `.stat`,
  `.ladder`, `.pyramid`, `.bars`, and tilts `.tilt-l` / `.tilt-r`) rather than
  inline styles, and avoid hard-coding colours in `index.qmd`. Keep the theme
  `simple` and the format `revealjs`.
- **Visual over text.** No large blocks of prose on a slide. Prefer tables,
  Mermaid diagrams, cards, and screenshots.
- **Spelling and punctuation.** Use British spelling in prose (colour, licence,
  catalogue, artefact) and the Oxford comma in lists of three or more. Leave
  code, identifiers, file names, URLs, quotations, and proper names (`license`
  in YAML, `.well-known/api-catalog`) as they are.
- **Image classes.** Screenshots use `.shot`; photos use `.photo`.
- **Sources and credits.** Every factual claim has a `.source` div at the
  bottom of its slide. Every third-party image has a `.credit` line under it
  **and** a row on the "Image credits" slide; screenshots record the capture
  date. Keep both in sync.
- **Code blocks.** Always tag the language (`bash`, `python`, `json`,
  `markdown`, `html`). Files with no Pandoc grammar (`robots.txt`, HTTP
  headers) use `{.default}` for plain text. Add `filename="…"` for a labelled
  header.
- **Spoken notes.** The read-aloud control speaks the `.notes` content. Write
  complete, audience-facing narration; keep staging cues, private reminders,
  and delivery checklists outside these blocks.
- **Accessibility.** Images must have `fig-alt` text; raw HTML widgets use
  `role="img"` and `aria-label`.
- **Icons.** Icons are HTML spans backed by only the required SVG path data in
  `style.css`; no icon font or Quarto icon extension. When adding one, add only
  its mask data, preserve the source licence attribution, and keep an
  accessible label where the icon conveys meaning.
- **Mermaid.** Keep diagrams as Mermaid source, never pre-rendered SVGs. Open
  every `{mermaid}` chunk with `%%| eval: true` and `%%| echo: false`: the
  document-level `execute` options apply to diagram chunks too, and without
  these overrides the diagram is suppressed and its source is printed instead.
  After those chunk options, start the diagram with
  `%%{init: {"htmlLabels": false, "flowchart": {"htmlLabels": false, "padding": 16}, "themeVariables": {"fontFamily": "Space Grotesk, sans-serif", "fontSize": "20px"}}}%%`:
  HTML labels are measured at the current zoom inside RevealJS's scaled slide
  and get clipped at other sizes. Never restyle Mermaid fonts from `style.css`,
  and avoid cylinder nodes (`[( )]`); they ignore padding.
- **MCP spec version.** All MCP content assumes the current, stateless spec
  ([2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28/changelog)):
  no `initialize` handshake, no `Mcp-Session-Id`, `server/discover` for
  capabilities, and `input_required` results instead of server-initiated
  requests. Do not teach handshake or session-era patterns, or the deprecated
  Roots, Sampling, and Logging features, and do not compare MCP with earlier
  revisions. When a newer revision ships, update the deck and re-verify
  examples against the MCP Python SDK.
- **No code execution.** The front matter sets `execute: eval: false`; code
  blocks are display-only. Do not enable `eval: true` unless the deck genuinely
  needs computed output.
- **Python dependencies.** The deck declares `jupyter: python3`; the virtualenv
  only satisfies Quarto's engine. Depend only on `ipykernel`, `nbclient` and
  `pyyaml`. Do not add the `jupyter` metapackage: it pulls in JupyterLab and
  Notebook and only attracts irrelevant security alerts.
- **Discoverability files.** Update `meta-tags.html` when the title,
  description, or social card changes, and `llms.txt` / `llms-full.txt` (and
  their `.well-known/` mirrors) when the content changes significantly.
- **No new top-level files** without a clear reason; the structure is flat.

## Pull requests

Follow these rules without relying on any instructions outside this
repository:

- Write every commit message and PR title as a Conventional Commit,
  `type(scope): description`, lowercase and imperative, with an allowed type
  (`build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`,
  `revert`, `style`, `test`). Keep the PR title and body in sync with the
  net diff.

- Open every PR ready for review with `gh pr create`, never as a draft.

- Never add agent or tool attribution to commits, PRs, or comments.

- When a PR needs visual evidence (such as slide layout or styling changes),
  use the shared `pr-screenshot` skill to post verified screenshots. Verify the
  uploaded images render in the comment.

- After opening or pushing, wait for hosted CI to finish. Inspect failed jobs,
  fix the cause, run the local checks, push, and repeat. Skipped, queued, or
  failing required checks are not success.

- If an automatic AI review (Codex, for the owner) runs on the PR, wait for
  its result instead of requesting one. Fix merited findings, reply to and
  resolve addressed threads, and continue until the review approves the
  current head with no unresolved findings. Never write `@codex` anywhere in
  a PR, even in backticks: it cancels the automatic review. Say "a Codex
  review request" instead.

- If Codex reports exhausted usage, take no workaround action: leave the PR
  open, do not merge, and report the review limit. CI work can still finish.
  Once usage refreshes, comment `@codex review` once; this is the only case
  that needs the comment.

- Once CI is green and the review gate is met, squash-merge with the owner's
  authenticated `gh` credentials, then verify the merged state. Recheck the
  head, threads, and checks immediately before merging, and never bypass
  branch protections.

- Update a PR branch from `main` only to resolve conflicts or pick up a change
  the PR depends on, never just to bring it up to date.

- Report local validation, hosted CI, review, and merge state separately. If
  an external blocker stops completion, leave the PR open and say so.

# CI/CD

- `.github/workflows/build-presentation.yaml` calls a reusable workflow from
  `IndrajeetPatil/workflows`. Do not inline or modify that workflow here.
- Reference `IndrajeetPatil/workflows` reusable workflows as `@main`, never a
  commit SHA. The owner maintains them and is the only person who can
  contribute to this repository, so there is no external-contributor risk, and
  `@main` keeps it on the latest version. Code scanners (CodeQL
  `actions/unpinned-tag`, zizmor `unpinned-uses`) flag this by design: do not
  report it or propose a pin; dismiss such alerts as "won't fix" with this
  reason.
