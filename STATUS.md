# STATUS — Calmer Gifting Printables

Last updated: 2026-10-26

## What was built

A complete, local-first pack of seven warm, print-ready gifting printables.
Each PDF opens with a warm "how to use it" page, then the sheet itself
(3 pages per PDF). The PDFs in `printables/` are unbranded — no names, no
logos, no links — and print cleanly in black & white on US Letter.

| Sheet (in `printables/`) | Purpose |
| --- | --- |
| `gift-idea-log.pdf` | Year-round gift-idea log ("note it when they mention it") + little-details page |
| `gift-budget-tracker.pdf` | Multi-person planned-vs-spent budget tracker + season totals |
| `handmade-vs-bought-planner.pdf` | Handmade/bought planner + friendly decision guide |
| `kids-wish-list.pdf` | Kids' ranked wish list + grown-up corner |
| `thank-you-note-templates.pdf` | Six fill-in-the-blank thank-you notes in kind wording |
| `holiday-week-checklist.pdf` | Day-by-day holiday-week checklist (with self-care baked in) |
| `cards-you-owe-tracker.pdf` | Cards tracker (picked/written/sent) + addresses at a glance |

Project layout:

- `src/*.html` + `src/base.css` — plain HTML/CSS sources, shared warm styling,
  CSS-drawn checkboxes and write-in lines (no images, no web fonts, no network).
- `build.py` — the one build script: renders every sheet to PDF with
  WeasyPrint, runs per-PDF sanity checks (header, page count, title metadata).
- `tests/test_build.py` — pytest suite that builds every sheet from source and
  verifies valid PDFs.
- `printables/` — the generated, ready-to-print PDFs (committed).
- `README.md`, `LICENSE` (MIT), `requirements.txt`.

## How to run it

```bash
pip install -r requirements.txt   # weasyprint, pypdf, pytest
python3 build.py                  # build all PDFs into printables/
python3 build.py --out DIR        # build into another directory
python3 build.py --only kids-wish-list   # build a single sheet
python3 -m pytest                 # run the test suite
```

Print the PDFs at 100% ("Actual size"), US Letter, portrait.

## Verification results (2026-10-26, this machine)

- `python3 build.py` from a clean `printables/`: **success**, all 7 PDFs built,
  each exactly 3 pages (usage page + 2 sheet pages).
- `python3 -m pytest`: **32 passed** in ~4.7s. Coverage includes: every sheet
  builds a real PDF (`%PDF` header, parses with pypdf), expected PDF title
  metadata, usage page first with print tips, 2–4 pages per sheet, no branding
  in any PDF's text ("Asdale", "Dylan", URLs all absent), `SHEETS` in
  `build.py` matches `src/*.html` exactly, CLI and in-process builds agree,
  and committed `printables/` is fresh and valid.
- `python3 -m py_compile build.py`: OK.
- Visual check: all 21 pages rendered to PNG and reviewed — layout, warm tone,
  checkbox alignment, and table fits confirmed (this caught and fixed three
  tables overflowing by one row, a wrapping header, and top-aligned checkboxes).

## Known gaps

- **US Letter only.** No A4 variant yet; A4 users should print with "Fit to
  page" or a scaled copy. Adding `src/base-a4.css` + a `--paper` flag would be
  the natural next step.
- **English only**, and the wording is warm/casual by design.
- **Row counts are fixed** (e.g., 16 rows in the idea log). More rows would
  need printing a second copy, or a follow-up "extended" variant.
- **Handwriting space is open-ruled**, not baseline-ruled; generous but not
  guided lines.
- **No usage-page-only variant** (e.g., a combined pack cover/index PDF) — the
  usage page ships inside each PDF instead.
- PDF creation dates differ per build (WeasyPrint default), so byte-for-byte
  rebuilds aren't reproducible; content is.
- Tested only on this Linux/Python 3.13/WeasyPrint 70 environment; WeasyPrint
  is the only renderer, so results elsewhere should match but weren't verified.
