# AGENTS.md

Project-level instructions for AI coding agents working on this repository —
Codex, GitHub Copilot (code review and coding agent), and other
`AGENTS.md`-aware tools read this file directly.

## What this is

A single-page [Quarto](https://quarto.org/) presentation rendered to [RevealJS](https://revealjs.com/) slides and deployed as a static site via GitHub Pages.

## Repository layout

```
index.qmd           # All slide content (the only file you usually need to edit)
_quarto.yml          # Quarto project config (output dir, resources list)
_quarto-a11y.yml     # Opt-in profile enabling the axe accessibility checker (`just axe`)
_brand.yml           # Brand tokens: colour palette and Space Grotesk / Space Mono fonts
accessibility.html  # Compatibility fixes supplementing the a11y extension
style.css            # Neo-brutalist component classes layered on _brand.yml
meta-tags.html       # OpenGraph, Twitter Card, JSON-LD, and analytics tags
justfile             # Command runner (install, render, preview, clean, etc.)
media/               # Images: evidence screenshots, illustrations, social card
llms.txt             # Short machine-readable summary for LLM discovery
llms-full.txt        # Extended machine-readable summary
.well-known/         # Mirrors of llms.txt and llms-full.txt
robots.txt           # Crawl rules
sitemap.xml          # Sitemap for search engines
LICENSE              # CC0 dedication for original content (third-party images excluded)
.github/             # CI workflow (reusable, from IndrajeetPatil/workflows) and Dependabot
_extensions/         # Latest a11y extension, installed by `just install` and CI (gitignored)
_site/               # Build output (gitignored)
```

### Language-specific files

Python-based decks also have:

```
pyproject.toml       # Project metadata and dependencies (managed by uv)
uv.lock              # Locked Python dependencies
.python-version      # Python version pin
.venv/               # Python virtualenv (gitignored)
```

R-based decks have instead:

```
renv.lock            # Locked R dependencies
renv/                # renv library and infrastructure (library/ is gitignored)
.Rprofile            # Bootstraps renv on session start
```

Check which set is present to know which language context applies.

## Key conventions

- **Single-file deck.** All slides live in `index.qmd`. There are no partial includes or multi-file splits.
- **Slide syntax.** Slides are separated by `##` headings. Use Quarto's RevealJS dialect: fenced divs (`:::`), columns (`.columns` / `.column`), raw HTML blocks (`{=html}`), and the `{.smaller}` class for dense slides.
- **Brand first.** Colours and fonts live in `_brand.yml` (Quarto brand.yml). `style.css` reads them as `--brand-*` custom properties and adds the neo-brutalist shapes: 3px ink borders, hard offset shadows, and slightly tilted cards, inspired by [loot-drop.io](https://www.loot-drop.io/). Add a colour to the brand palette before using it anywhere else; avoid inline `style` colours.
- **Component classes.** Use the existing classes rather than inline styles: `.card` (with colour modifiers `.yellow`, `.green`, `.pink`, `.amber`, `.cream`, `.ink`, `.forest`, and `.red`; tilts `.tilt-l` / `.tilt-r`), `.grid-2|3|4`, `.callout-big`, `.tag`, `.sticker`, `.stat`, `.ladder`, `.pyramid`, `.bars`, and `.code-sm` for dense code. Section dividers are `#` headings with `background-color="#FFD600"`.
- **Visual over text.** No large blocks of prose on a slide. Prefer tables, Mermaid diagrams, cards, and screenshots.
- **Spelling and punctuation.** Use British spelling in prose (colour, licence, catalogue, artefact) and the Oxford comma in lists of three or more. Leave code, identifiers, file names, URLs, quotations, and proper names (`license` in YAML, `.well-known/api-catalog`) as they are.
- **Image classes.** Screenshots use `.shot`; photos use `.photo`. Both get ink borders and shadows in `style.css`.
- **Sources and credits.** Every factual claim has a `.source` div at the bottom of its slide. Every third-party image has a `.credit` line under it **and** a row on the "Image credits" slide; screenshots record the capture date. Keep both in sync.
- **Code blocks.** Always tag the language (`bash`, `python`, `json`, `markdown`, `html`). Files with no Pandoc grammar (`robots.txt`, HTTP headers) use `{.default}` for plain text. Add `filename="…"` for a labelled header.
- **Accessibility.** Images must have `fig-alt` text. Raw HTML widgets use `role="img"` and `aria-label`. Keep these.
  Verify with `just axe`, which appends an "Accessibility Report" slide listing axe-core violations. Do not add `axe` to
  `index.qmd`: it belongs in `_quarto-a11y.yml` so the deployed deck never ships the axe-core payload. Note that
  `-M axe:true` cannot enable it, because the `format:` block in `index.qmd` takes precedence over CLI metadata.
  Links inside muted text need a non-colour cue (e.g. `text-decoration: underline`) to satisfy WCAG 1.4.1.
  The `a11y` extension supplies zoom, focus indicators, link underlines, reduced motion,
  slide isolation, and screen-reader announcements. Keep `accessibility.html` for
  code scrolling, menu focus, and vertical-slide semantics. This deck has no
  tabsets, but `accessibility.html` still ships the shared tabset keyboard handling:
  the file is copied verbatim across decks and kept in sync by hand, so never trim
  it locally.
  Version 0.2.3's slide-menu patch and settings menu introduce axe failures on this
  deck, so both are disabled in `index.qmd`. Inspect all slides,
  revealed fragments and menu panels in both presentation and native `?view=scroll` modes;
  the initial report alone does not exercise every state. For headless checks, use
  `just axe --no-browser --port 8891`.
- **Icons.** Icons use lightweight HTML spans backed by only the required SVG path data in the custom stylesheet; no icon-font or Quarto icon extension is needed.
  When adding an icon, add only its mask data, preserve the source licence attribution, keep an accessible label where the icon conveys meaning, and render the deck to verify it.
- **Mermaid labels.** Start every Mermaid diagram with
  `%%{init: {"htmlLabels": false, "flowchart": {"htmlLabels": false, "padding": 16}, "themeVariables": {"fontFamily": "Space Grotesk, sans-serif", "fontSize": "20px"}}}%%`.
  Quarto renders diagrams on page load inside RevealJS's scaled slide, so HTML labels are measured at the
  current zoom and get clipped (or float in oversized boxes) at other window sizes. SVG text labels are
  measured in the diagram's own units and stay correct at any scale. Never restyle Mermaid fonts from
  `style.css`: a font swap after measurement clips labels. Avoid cylinder nodes (`[( )]`); they ignore
  padding and hug their text.
- **MCP spec version.** All MCP content assumes the current, stateless spec
  ([2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28/changelog)): no
  `initialize` handshake, no `Mcp-Session-Id`, `server/discover` for capabilities, and
  `input_required` results instead of server-initiated requests. Do not teach handshake or
  session-era patterns, or the deprecated Roots, Sampling, and Logging features. Describe MCP
  as it is now; do not compare it with earlier revisions, since most of the audience is
  meeting MCP for the first time. When a newer
  revision ships, update the deck and re-verify examples against the MCP Python SDK.
- **Mermaid performance boundary.** Keep Mermaid diagrams as Mermaid source. Do not replace them with pre-rendered SVGs solely to reduce the website bundle.
- **No code execution.** The YAML front matter sets `execute: eval: false`. Code blocks are for display only; they are not executed during render.
- **Compute engine.** Python decks declare `jupyter: python3` in the front matter; R decks declare `engine: knitr`. The virtualenv or renv exists to satisfy Quarto's engine, not to run slide code. Python decks depend only on what Quarto's Jupyter engine imports: `ipykernel`, `nbclient` (which brings `nbformat` and `jupyter-client`), and `pyyaml`. Do not add the `jupyter` metapackage: it pulls in JupyterLab and Notebook, which the deck never runs, and only attracts irrelevant security alerts.

## Commands

All commands use [just](https://github.com/casey/just). The recipes are the same across decks; only the dependency backend differs:

```bash
just install   # Install language dependencies and the latest a11y extension
just sync      # Alias for install
just update    # Update language dependencies
just render    # Render index.qmd to _site/
just preview   # Live-reload dev server
just open      # Alias for preview (live-reload dev server over localhost)
just clean     # Remove build artefacts
just check     # Verify Quarto setup
just axe       # Preview with the axe accessibility checker enabled
```

This deck renders with Quarto. Python dependencies are managed with [uv](https://docs.astral.sh/uv/) (`pyproject.toml` + `uv.lock`); CI installs them with `uv sync --frozen`. Slides live in `index.qmd`.

## Editing slides

When modifying `index.qmd`:

1. Follow the existing card/column layout patterns visible in neighbouring slides.
2. Preserve the source-citation div at the bottom of each slide.
3. Use the established background-colour palette for info cards rather than inventing new colours.
4. Keep `fig-alt` on every image and `aria-label` on HTML widgets.
5. Run `just render` (or `just preview`) to verify changes compile without errors.

## Editing styles

`style.css` defines CSS custom properties under `:root` and component classes for complex HTML widgets. The variable names and widget classes vary per deck. When adding a new widget, follow the naming and structure patterns already present in the file.

## SEO and discoverability files

- `meta-tags.html` contains OpenGraph, Twitter Card, JSON-LD structured data, and Google Analytics. Update it when the title, description, or social card image changes.
- `llms.txt` and `llms-full.txt` are machine-readable summaries following the llms.txt convention. Update them when the deck content changes significantly.
- `sitemap.xml` and `robots.txt` are static and rarely need changes.

## CI/CD

- The GitHub Actions workflow in `.github/workflows/` renders the deck and deploys to GitHub Pages. Pushes to `main` build and deploy; pull requests build the deck as a check, and `workflow_dispatch` allows a manual run. It calls a reusable workflow from `IndrajeetPatil/workflows` (Python and R decks use different workflow files). Do not inline the workflow.
- **Reference the reusable workflow as `@main`, not a commit SHA.** These workflows are first-party, so tracking `main` is intentional: upstream fixes arrive immediately instead of waiting on a manual SHA bump. A previously pinned SHA went five months stale, leaving CI building with pre-release Quarto and installing a FontAwesome extension this deck does not use, long after upstream had fixed both. Dependabot cannot bump a branch ref, so there is nothing to keep in sync.
- Install the latest a11y extension directly from upstream with
  `quarto add mcanouil/quarto-revealjs-a11y --no-prompt` in both `justfile` and CI.
  This extension is trusted; do not add version pins, vendoring, or checksum checks.
- Dependabot keeps GitHub Actions dependencies up to date weekly. Python decks also have Dependabot configured for `uv`; R decks do not use Dependabot for R packages.

## What not to do

- Do not add new top-level files without a clear reason; the project intentionally has a flat structure.
- Do not split `index.qmd` into multiple files.
- Do not change the Quarto theme from `simple` or the output format from `revealjs`; restyle through `_brand.yml` and `style.css`.
- Do not enable code execution (`eval: true`) unless the presentation genuinely needs computed output.
- Do not commit `_site/`, `_extensions/`, or `.quarto/` (all gitignored). For Python decks, `.venv/` is also gitignored; for R decks, `renv/library/` and `renv/staging/` are gitignored.
- Do not modify the reusable CI workflow inline; it lives in a separate repository.
- Do not pin the reusable workflow to a commit SHA; use `@main` (see CI/CD).
