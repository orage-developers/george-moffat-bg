# Verification

Use your own temporary check folder (`$CHECK`), such as the session
scratchpad or `mktemp -d`. Never use the output folder: the review PDF would
overwrite the delivered PDF. Look at every page, not only the first, at
70 dpi or more.

## Checks

- PDF: `head -c 4 file.pdf` prints `%PDF`. Rasterize and look at the pages:
  ```bash
  pdfinfo file.pdf | grep Pages
  pdftoppm -r 70 -png file.pdf "$CHECK/p"
  ```
- DOCX and PPTX: convert them to PDF for review only and look at the pages.
  This LibreOffice render is a proxy for Google Docs and Slides: check
  content, colors, fonts and order, not exact line breaks or page count.
  ```bash
  soffice --headless --convert-to pdf --outdir "$CHECK" file.docx
  pdftoppm -r 70 -png "$CHECK/file.pdf" "$CHECK/p"
  ```
- Fonts: in every delivered PDF, `pdffonts` lists only Anton and
  BebasNeue. Any other font means a glyph the brand fonts lack or a
  misspelled family. The LibreOffice review renders of DOCX and PPTX may
  also list OpenSymbol for list bullets; that is fine.
- Colors: `grep -ci '#000000' file.html` prints 0, and the HTML uses only
  the greyscale in [brand.md](brand.md) (no gold, no hue).
- PPTX: the slide count equals the number of slide sections:
  `grep -c '^ *<section class="slide' file.html` and
  `unzip -l file.pptx | grep -c 'ppt/slides/slide[0-9]*.xml'` print the same
  number.
- XLSX: export every sheet to CSV (one file per sheet) and check values and
  computed formulas:
  ```bash
  soffice --headless --convert-to 'csv:Text - txt - csv (StarCalc):44,34,76,1,,0,false,true,false,false,false,-1' \
    --outdir "$CHECK" file.xlsx
  ```
- CSV: `head` the file; check accents and the delimiter.
- Comparisons: recompute one change and one % change by hand and match them
  against the table, the chart labels and the headline.

## Common errors

- `LibreOffice produced no output`: the HTML is missing or has an encoding
  error. Always save UTF-8 with `<meta charset="utf-8">`.
- `Chrome/Chromium not found`: install Chrome or set `CHROME_BIN`.
- Wrong fonts in DOCX: the font was not declared on every selector.
- Bold text in DOCX: a `font-weight` other than `normal` or a `<b>` tag.
  Both brand fonts have one weight; emphasis is white, not bold.
- LiberationSans or another extra font in `pdffonts`: a glyph Bebas Neue
  lacks (`→`, `■`, `●`), or a margin-box footer using a font the body does
  not use.
- White page in DOCX: `bgcolor` is missing on `<body>`.
- Bars without color in the PDF: a CSS rule overrides `bgcolor`; add an
  inline `style="background:…"`.
- Grey boxes behind slide titles in PPTX: `text-shadow` or `box-shadow` on
  a slide. Glow is for documents only.
- Extra slides in PPTX: a `.slide` overflows or content sits outside the
  sections.
- Heading alone at the bottom of a PDF page: the heading lost
  `break-after: avoid`.
