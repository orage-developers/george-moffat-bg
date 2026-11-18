# Brand

Every file follows the George W. Moffat personal brand, unless the request
explicitly names another brand (for Orage AI Agency files, use the Orage
skill). Read `BRAND-GUIDELINES.md` in full before you write the HTML. Take
the voice, typography, show format and identity from it. Take colors from
this rule: this palette replaces the color section of the guidelines for
every file this skill makes.

Never invent audience numbers, results, prices, guests or contact details
that are not in the guidelines or the request. Mark sample data as sample
data.

## Palette

Monochrome: black backgrounds, white as the only accent, greys for
hierarchy. Tokens are in `brand/tokens.css`. Use no other colors: no gold,
no hue of any kind.

| Role | Color | Use |
|---|---|---|
| Background | `#010101` | Page and slide background |
| Raised | `#070707` | Cover slides, raised panels |
| Card | `#0C0C0C` | Cards, boxes, table cells |
| Elevated | `#151515` | Table headers, meta labels |
| White accent | `#FFFFFF` | Titles, key numbers, emphasis, lead item bar |
| Ink bright | `#C8C8C8` | Body text |
| Grey mid | `#8A8A8A` | Eyebrows, meta, notes, footer |
| Grey dim | `#5A5A5A` | Captions, slide footers |
| Grey faint | `#333333` | Section rules, the thin half of a title, standard card bars |
| Line | `#262626` | Card and table borders |
| Chart series 1 | `#8A8A8A` | Baseline or earlier period |
| Chart series 2 | `#FFFFFF` | Main or later period |

**Never `#000000`.** The darkest color is `#010101`.

Emphasis comes from white, glow and scale, never from color or bold:
`<strong>` and `.key` are white with a soft `text-shadow` glow. Glow shows
only in the PDF, and never goes on slides (see
[format-pptx.md](format-pptx.md)).

## Fonts

- **Two fonts, never a third**: Anton for the heaviest display moments (H1,
  the wordmark, big numbers, prices, the signature name); Bebas Neue for
  everything else (H2, H3, eyebrows, body, tables, buttons, captions).
- Both have one weight. Use `font-weight: normal` everywhere and never
  `<b>`: bold would be faked.
- Everything is uppercase. Bebas Neue has no lowercase, so its text always
  reads uppercase. Anton has lowercase: **type Anton text in UPPERCASE** in
  the HTML (`<h1>DAILY REPORT</h1>`), since Google Docs may drop
  `text-transform`.
- Both are Google Fonts, so Google Docs, Slides and Sheets show them without
  installing anything.
- Bebas Neue has no `→`, `■` or `●`. Put `→` and `■` in Anton:
  `<span class="arrow">→</span>`. Write `to` instead of an arrow inside
  Bebas text, and avoid `●`. Otherwise a third fallback font appears.
- The templates already declare the `@font-face` rules.

## Header

- The brand has no logo image. The header is the "GEORGE W. MOFFAT"
  wordmark in Anton, white, with no background.
- Documents and data files use the compact header: the wordmark at 11pt,
  right-aligned. `comparison-report.html` and `comparison-data.html` use the
  larger, left-aligned header with the tagline "The AI Rundown · Orage AI
  Agency" in grey.
- Decks put "George W. Moffat" in the cover eyebrow and in the footer of
  every content slide. Cover and closing slides have no footer.

## Voice

- Direct, authoritative, results-first, high-status calm. A senior operator
  handing over the takeaway, not a creator begging for the click.
- Lead with the result. Cut every line by 30%.
- No hype words ("revolutionary", "game-changing", "insane").
- No emoji anywhere.
- One clear ask per file, and every file points back to Orage AI Agency
  (footer, signature or CTA).

## Footer

PDF documents carry "GEORGE W. MOFFAT · THE AI RUNDOWN · ORAGE AI AGENCY"
(already in the templates). DOCX has no footer; that is fine.

## `brand://` URLs

In the HTML, `brand://<path>` points to the skill's `brand/` folder. The
script resolves it on every conversion.

```html
<style>
  @font-face { font-family: "Anton"; src: url("brand://fonts/Anton-Regular.ttf"); }
</style>
```

For DOCX and PPTX the script installs the brand fonts in the user font
folder (`~/.local/share/fonts/george-moffat-brand` on Linux,
`~/Library/Fonts` on macOS) when they are missing, so the conversion
measures text with the real fonts.

## Brand folder

`BRAND-GUIDELINES.md` sits at the skill root. `brand/` holds `tokens.css`
and `fonts/` (Anton, Bebas Neue, OFL licenses).
