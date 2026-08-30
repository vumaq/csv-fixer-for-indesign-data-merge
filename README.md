# CSV Fixer for InDesign Data Merge

A single-page, no-build web tool that cleans up a CSV so InDesign's Data
Merge actually opens it cleanly. Drop a file in, review what's wrong,
untick anything you don't want fixed, then copy or download the result.
No signup, no server — everything runs client-side in the browser.

## Why

![InDesign Data Merge Import Error](https://vumaq.github.io/csv-fixer-for-indesign-data-merge/indesign-csv-import-error.png)

InDesign Data Merge is fussy about CSV formatting, and the failures are
usually silent rather than an error message: fields quietly shift into the
wrong column, a duplicate header collapses two fields into one, or a
character that should be `é` comes back as `Ã©`. This tool detects and
fixes the common causes.

## What it fixes

| Problem | What it does | Toggle |
|---|---|---|
| UTF-8 BOM | Excel/some editors prepend an invisible byte-order mark, which gets read as part of the first header name (`Code` becomes `\uFEFFCode`) | Yes |
| Non-CRLF line endings | Data Merge is more reliable with Windows-style line endings; mixed/LF-only endings can drop or merge the last row | Yes |
| Semicolon delimiter | European-locale Excel exports use `;` instead of `,` — otherwise the file loads as one giant column | Yes |
| Blank rows | Fully empty rows, anywhere in the file (not just a trailing one) | Yes |
| Stray whitespace | Leading/trailing spaces in headers or values silently break field matching | Yes |
| Blank column headers | A column with no name can't be targeted as a merge field | Yes |
| Duplicate column headers | Two columns sharing a name collapse into a single mergeable field | Yes |
| Ragged rows | A row with more/fewer fields than the header row shifts every later value into the wrong column — detected and auto-aligned automatically, no toggle needed |
| `@`-prefixed headers | Not fixed, just flagged — Data Merge treats a column named `@Photo` as an image field, not text |

Every fix has a status badge showing exactly what was found in your file
and whether it's currently being fixed. Download and Copy stay disabled
until every detected issue is either fixed or doesn't apply — so what you
export is guaranteed clean, not just "probably fine."

## Using it

Open `index.html` in a browser — no server, no build step, no
dependencies to install. Drag a `.csv` onto the drop zone (or click to
browse), review the diagnostics, untick anything you don't want changed,
then Copy or Download the result. Long CSVs scroll inside the preview
panel rather than growing the page.

## Privacy

Parsing, fixing, and exporting all happen in the browser with plain
JavaScript. The CSV never leaves your machine — there's no server-side
component at all.

## License

MIT (or update this to whatever you prefer).
