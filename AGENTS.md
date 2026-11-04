# AGENTS.md

A single-page [Quarto](https://quarto.org/) presentation rendered to
[RevealJS](https://revealjs.com/) slides and deployed as a static site via
GitHub Pages.

## Repository layout

```text
index.qmd            # All slide content (the only file you usually need to edit)
_quarto.yml          # Quarto project config (output dir, resources list)
_quarto-a11y.yml     # Opt-in profile enabling the axe accessibility checker (`just axe`)
_brand.yml           # Brand tokens: colour palette and Space Grotesk / Space Mono fonts
accessibility.html   # Compatibility fixes supplementing the a11y extension
style.css            # Neo-brutalist component classes layered on _brand.yml
meta-tags.html       # OpenGraph, Twitter Card, JSON-LD, and analytics tags
justfile             # Command runner
media/               # Images: evidence screenshots, illustrations, social card
llms.txt, llms-full.txt   # Machine-readable summaries (mirrored in .well-known/)
robots.txt, sitemap.xml   # Static crawl files; rarely change
pyproject.toml, uv.lock   # Python dependencies for Quarto's Jupyter engine (uv)
LICENSE              # CC0 for original content (third-party images excluded)
```

`_site/`, `_extensions/`, `.quarto/` and `.venv/` are gitignored; never commit
them.

## Commands

```bash
just install   # Install Python dependencies and Quarto extensions
just update    # Update Python dependencies
just render    # Render index.qmd to _site/ (run after every change)
just preview   # Live-reload dev server
just clean     # Remove build artefacts
just check     # Verify Quarto setup
just axe       # Preview with the axe accessibility checker enabled
```

## Key conventions

- **Single-file deck.** All slides live in `index.qmd`; do not split it. Slides
  are separated by `##` headings. Use Quarto's RevealJS dialect: fenced divs
  (`:::`), columns (`.columns` / `.column`), raw HTML blocks (`{=html}`), and
  the `{.smaller}` class for dense slides. Follow the layout patterns of
  neighbouring slides.
- **Brand first.** Colours and fonts live in `_brand.yml`. `style.css` reads
  them as `--brand-*` custom properties and adds the neo-brutalist shapes: 3px
  ink borders, hard offset shadows, and slightly tilted cards. Add a colour to
  the brand palette before using it anywhere else; avoid inline `style`
  colours. Keep the theme `simple` and the format `revealjs`.
- **Component classes.** Use the existing classes rather than inline styles:
  `.card` (with colour modifiers `.yellow`, `.green`, `.pink`, `.amber`,
  `.cream`, `.ink`, `.forest`, and `.red`; tilts `.tilt-l` / `.tilt-r`),
  `.grid-2|3|4`, `.callout-big`, `.tag`, `.sticker`, `.stat`, `.ladder`,
  `.pyramid`, `.bars`, and `.code-sm` for dense code. Section dividers are `#`
  headings with `background-color="#FFD600"`. New widgets follow the naming
  patterns already in `style.css`.
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
  `role="img"` and `aria-label`. Load the `check-accessibility` skill before
  changing markup, styles, widgets or the a11y setup.
- **Icons.** Icons are HTML spans backed by only the required SVG path data in
  `style.css`; no icon font or Quarto icon extension. When adding one, add only
  its mask data, preserve the source licence attribution, and keep an
  accessible label where the icon conveys meaning.
- **Mermaid.** Keep diagrams as Mermaid source, never pre-rendered SVGs. Start
  every diagram with
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

## CI/CD

- `.github/workflows/` calls a reusable workflow from `IndrajeetPatil/workflows`:
  pushes to `main` build and deploy to GitHub Pages, pull requests build as a
  check. Do not inline or modify that workflow here.
- Reference the reusable workflow as `@main`, never a commit SHA: it is
  first-party, and a pinned SHA once went five months stale.
- Dependabot updates GitHub Actions and `uv` dependencies weekly.

## Agent skills

Skills live in `.agents/skills/<name>/SKILL.md`. Load one before its task:

| Skill | Load before |
| --- | --- |
| `check-accessibility` | Changing slide markup, styles, widgets, menus or the a11y setup; any accessibility audit |
