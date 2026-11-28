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

## Agent tool loop: `agent-tool-loop.webp`

```text
Use case: infographic-diagram
Asset type: raster flowchart for a Quarto RevealJS presentation.
Primary request: show an agent's goal-driven Think, Act, Observe loop, matching a neo-brutalist software presentation. Diagram only, no title.
Scene/backdrop: solid flat paper #FAFAF5. Portrait canvas approximately 4:5 with modest outer margins.
Style: crisp flat graphic; heavy #0A0A0A ink outlines; hard black shadows offset down and right; very slight card tilts; bold Space Grotesk-style sans-serif headings and Space Mono-style smaller subtitles. Palette restricted to paper #FAFAF5, cream #F5F5F0, ink #0A0A0A, yellow #FFD600, green #00C853. No gradients, texture, 3D or decorative clutter.
Composition: five centered vertically stacked nodes, with clearly visible black downward arrowheads and comfortable breathing room: a rounded white "Goal from a human" card at top; a cream "Think" card with subtitle "pick the next step"; a yellow "Act" card with subtitle "call a tool"; a cream "Observe" card with subtitle "read the output"; a rounded green "Done" card at bottom. A single large separate return connector emerges from the LEFT edge of Observe, runs outside the cards to the left, then turns right with its arrowhead entering the LEFT edge of Think. Ensure this direction is Observe back to Think. The Observe-to-Done arrow continues downward. Exactly these six arrows: Goal to Think, Think to Act, Act to Observe, Observe to Think, Observe to Done. (Five arrows in total.) No other connections. All connectors avoid shadows and label areas.
Text (verbatim): "Goal from a human"; "Think"; "pick the next step"; "Act"; "call a tool"; "Observe"; "read the output"; "Done".
Constraints: all labels exact, large readable type suitable for the left half of a presentation slide. Entire chart fits in frame. Keep the left return loop legible. No icons, extra labels, numbering, source, watermark, or frame.
```

## Slide: `three-ways-in.webp`

Generated with the built-in image generation tool on 28 November 2026, then converted to WebP with `cwebp -q 90 -m 6`.

```text
Create a wide landscape editorial illustration for a presentation slide, following a neo-brutalist visual system. Flat warm paper background (#FAFAF5); heavy black ink outlines (#0A0A0A); hard, crisp black offset shadows; bright yellow (#FFD600), vivid green (#00C853), and pink (#FF4081) accents; simple geometric shapes; bold, clean forms; generous negative space; slightly tilted paper cards, no gradients, no texture, no 3D, no photorealism. Scene: one shared software product represented by a large central black-outlined yellow hub, with three distinct pathways connecting to it from three small interface stations arranged clearly across the top: (1) a clean HTTP request/document symbol, (2) a terminal prompt symbol, (3) linked nodes representing a tool server. From the hub, one clear arrow leads to a small AI agent symbol on the right, with a tiny person icon behind it to imply delegated use. Make every path visually distinct, balanced and easy to parse at a glance, avoid overlapping shapes, keep substantial spacing between every outlined object and its hard shadow. Do not include any words, letters, numbers, logos, frames, badges, or captions. All objects fully inside the image.
```
