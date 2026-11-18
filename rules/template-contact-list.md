# Template: Contact list

- **File**: `templates/contact-list.html`
- **Formats**: CSV (primary), XLSX, PDF
- **Use for**: guest, sponsor, contact or lead lists.
- **Also follow**: [format-csv.md](format-csv.md).

## Structure

One table, `data-sheet="Contacts"`: `Name`, `Company`, `Email`, `Phone`,
`Type` (Guest, Sponsor, Lead), `Source`, `Stage`.

## Content

- Phones, ZIP codes and IDs use `data-type="text"` to keep leading zeros.
- Mark sample data in the caption (`Contacts · [List] · Sample data`) and
  use clearly fake details (`example.com` emails, `555` numbers).
