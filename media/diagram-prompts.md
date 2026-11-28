# Illustration prompts

Prompts for original raster illustrations in the presentation. Each image's generation and conversion details appear with its prompt.

## Same product, new user: `product-user-paths.webp`

```text
Use case: infographic-diagram
Asset type: wide raster diagram for a Quarto RevealJS presentation.
Primary request: recreate this exact two-row flowchart in the project's neo-brutalist brand. Diagram only, no slide title.
Scene/backdrop: flat solid paper #FAFAF5, clean generous margins, wide landscape canvas approximately 2.6:1.
Style: crisp flat graphic, heavy #0A0A0A ink outlines, hard black shadows offset down and right, very slight card tilts, Space Grotesk-style bold sans-serif labels and Space Mono-style small labels. No gradients, texture, 3D or decorative clutter.
Palette: paper #FAFAF5, cream #F5F5F0, ink #0A0A0A, pink #FF4081, yellow #FFD600, green #00C853.
Composition: two horizontal rows with clear left-to-right arrows. Both rows start at the same left edge and end with matching green product cards aligned at the same right edge. Top row has three nodes: white rounded Human card -> cream GUI card -> green Your product card. Bottom row has four nodes: white rounded Human card -> pink AI agent card -> yellow Text interfaces card -> green Your product card. Adjust widths to leave clear arrow space; bottom labels stay legible. Thick black single-headed arrows point right, never cross labels or touch text.
Text (verbatim): top row "Human"; "GUI" with subtitle "buttons, forms, pages"; "Your product". Bottom row "Human"; "AI agent"; "Text interfaces" with subtitle "CLI, MCP, API, Markdown"; "Your product".
Constraints: preserve all six forward connections, exactly seven nodes, all text exact and large enough for a presentation. No extra captions, icons, row labels, source, watermark or frame. Leave only modest outer margins. Entire diagram in frame.
```

## Slide: `machine-visitors-infographic-wide.webp`

Generated with the built-in image generation tool on 28 November 2026, then converted to WebP with `cwebp -q 92`.

```text
Use case: infographic-diagram
Asset type: wide infographic for a Quarto RevealJS presentation slide
Primary request: A well-labelled illustration that replaces a table about four kinds of machine visitors to websites. Preserve all four categories, example user-agent names, purposes, and timing.
Scene/backdrop: Flat warm paper #FAFAF5.
Subject: Four sections in a 2-by-2 arrangement:
1. SEARCH CRAWLER. Examples: Googlebot, OAI-SearchBot, Claude-SearchBot. Purpose: Index pages for search results. Timing: Continuously.
2. TRAINING CRAWLER. Examples: GPTBot, ClaudeBot, CCBot. Purpose: Collect content for model training. Timing: Periodically.
3. USER-DIRECTED FETCHER. Examples: ChatGPT-User, Claude-User, Perplexity-User. Purpose: Answer one person's question now. Timing: On demand.
4. BROWSER AGENT. Examples: Claude-Agent, standard Chrome user agent. Purpose: Click and type on a user's behalf. Timing: On demand.
Style/medium: Editorial infographic in the presentation's neo-brutalist print style: Space Grotesk-like bold sans-serif headings, readable mono-like metadata, heavy black outlines, hard offset black shadows, simple line pictograms, and flat fills.
Composition/framing: Extra-wide 16:9 landscape. Each section uses a small pictogram at left and clearly aligned text to its right. Keep the full composition low in height so it fits below a slide title and above a short source line and takeaway. Text should occupy most of each panel's width and remain large and readable.
Color palette: Paper #FAFAF5, ink #0A0A0A, grey #4B5563, yellow #FFD600, green #00C853, amber #F59E0B, blue #2563EB, and pink #FF4081. Give each section a distinct flat accent fill and neutral ink outlines.
Text (verbatim): Use the four labels, example lists, purpose, and timing exactly as specified above. Write field labels as Examples, Purpose, and Timing. No extra copy.
Constraints: Keep the four types distinct. All text must fit inside its own panel without touching borders or shadows. Large readable type, clean punctuation, exact names, sufficient padding.
Avoid: 4:3 or square layout, overlaps, tiny text, company logos, gradients, glows, soft shadows, photorealism, UI mockups, extra text, and watermarks.
```

## Slide: `three-ways-in.webp`

Generated with the built-in image generation tool on 28 November 2026, then converted to WebP with `cwebp -q 90 -m 6`.

```text
Create a wide landscape editorial illustration for a presentation slide, following a neo-brutalist visual system. Flat warm paper background (#FAFAF5); heavy black ink outlines (#0A0A0A); hard, crisp black offset shadows; bright yellow (#FFD600), vivid green (#00C853), and pink (#FF4081) accents; simple geometric shapes; bold, clean forms; generous negative space; slightly tilted paper cards, no gradients, no texture, no 3D, no photorealism. Scene: one shared software product represented by a large central black-outlined yellow hub, with three distinct pathways connecting to it from three small interface stations arranged clearly across the top: (1) a clean HTTP request/document symbol, (2) a terminal prompt symbol, (3) linked nodes representing a tool server. From the hub, one clear arrow leads to a small AI agent symbol on the right, with a tiny person icon behind it to imply delegated use. Make every path visually distinct, balanced and easy to parse at a glance, avoid overlapping shapes, keep substantial spacing between every outlined object and its hard shadow. Do not include any words, letters, numbers, logos, frames, badges, or captions. All objects fully inside the image.
```
