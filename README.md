# George W. Moffat html-to-files skill

An agent skill that creates DOCX, PPTX, PDF, XLSX and CSV files in the
George W. Moffat personal brand (The AI Rundown). Every file starts as an
HTML page built from a branded template and is converted with one script.
The output is meant mainly for Google Workspace: DOCX opens in Google Docs,
PPTX in Google Slides, and XLSX and CSV in Google Sheets.

Agents read [SKILL.md](SKILL.md). This README is for the people who install
and maintain the skill. Orage AI Agency files use the separate Orage skill,
which has the same structure.

## Layout

| Path | Contents |
|---|---|
| `SKILL.md` | Entry point for agents: always follow the brand guidelines and the rules, plus the rules index |
| `BRAND-GUIDELINES.md` | Personal brand book: identity, voice, typography, palette, components, show anatomy, non-negotiables |
| `rules/` | One Markdown rule per topic: brand, workflow, verification, comparisons, each format and each template |
| `templates/` | Branded HTML templates, one per kind of document |
| `scripts/html2file.py` | Converts an HTML file to PDF, DOCX, PPTX, XLSX or CSV |
| `brand/` | `tokens.css` and the fonts (Anton, Bebas Neue) |

## Requirements

- Python 3.9 or newer (standard library only).
- Google Chrome or Chromium for PDF and PPTX.
- LibreOffice (`soffice`) for DOCX and PPTX.
- Poppler (`pdftoppm`, `pdfinfo`, `pdffonts`) for the verification steps.

Set `CHROME_BIN` or `SOFFICE_BIN` when the binaries are not on `PATH`, and
`CHROME_NO_SANDBOX=1` inside containers without a sandbox.

## Install

Clone the repository and link it into the agent's skills folder. For Claude
Code:

```bash
git clone <repository-url> george-moffat
ln -s "$PWD/george-moffat" ~/.claude/skills/george-moffat-html-to-files
```

The first DOCX or PPTX conversion installs the brand fonts in
`~/.local/share/fonts/george-moffat-brand` (Linux) or `~/Library/Fonts`
(macOS) when they are missing.

## Usage

```bash
cp templates/report.html out/report.html
# edit out/report.html
python3 scripts/html2file.py out/report.html --to docx
python3 scripts/html2file.py out/report.html --to pdf
```

Each call writes the file next to the HTML with the new extension, or to the
path given with `-o`. Run `python3 scripts/html2file.py --help` for the CSV
options.

## Templates

| Template | Formats |
|---|---|
| `document.html` | DOCX, PDF |
| `report.html` (status report) | DOCX, PDF |
| `comparison-report.html` (period vs period) | DOCX, PDF |
| `proposal.html` | DOCX, PDF |
| `one-pager.html` (The AI Rundown) | PDF, DOCX |
| `letter.html` | DOCX, PDF |
| `slides.html` | PPTX, PDF |
| `pitch-deck.html` (The AI Rundown) | PPTX, PDF |
| `data.html` | XLSX, CSV, PDF |
| `comparison-data.html` (period vs period) | XLSX, CSV, PDF |
| `tracker.html` (episode tracker) | XLSX, PDF |
| `contact-list.html` (guests, sponsors) | CSV, XLSX, PDF |

Each template has a rule in `rules/template-<name>.md` that describes its
structure and content.

## Brand at a glance

- Monochrome. Backgrounds `#010101`, `#070707`, `#0C0C0C`, `#151515`; white
  `#FFFFFF` as the only accent; greys `#C8C8C8`, `#8A8A8A`, `#5A5A5A`,
  `#333333` for hierarchy. Never `#000000`, never gold or any hue.
- Anton for display, Bebas Neue for everything else. Always uppercase. No
  third font.
- Full rules: [rules/brand.md](rules/brand.md) and
  [BRAND-GUIDELINES.md](BRAND-GUIDELINES.md).

## Maintaining

- Change a template's HTML and its rule in `rules/` together.
- Add a new template with a matching `rules/template-<name>.md` and a row in
  the `SKILL.md` index.
- Check every change with the steps in
  [rules/verification.md](rules/verification.md).
