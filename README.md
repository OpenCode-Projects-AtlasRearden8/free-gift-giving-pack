# Calmer Gifting Printables

Free, warm, print-ready PDF helpers for calmer, kinder gift-giving. Seven
printable sheets you can print at home, fill in with a pen, and tape to the
fridge. The PDFs are unbranded, work in black & white, and everything is built
locally from plain HTML/CSS — no accounts, no tracking, nothing online.

## What's inside (`printables/`)

| PDF | What it's for |
| --- | --- |
| `gift-idea-log.pdf` | Year-round gift-idea log — note it when they mention it, plus a "little details" page (sizes, favorites, hobbies). |
| `gift-budget-tracker.pdf` | Multi-person gift-budget tracker: planned vs. spent per person, plus a season totals page. |
| `handmade-vs-bought-planner.pdf` | Handmade-vs-bought planner with a friendly decision guide and start-by dates. |
| `kids-wish-list.pdf` | A kids' wish-list sheet with room to rank wishes, explain them, and dream a little. |
| `thank-you-note-templates.pdf` | Fill-in-the-blank thank-you notes in kind wording — including for the trickier moments. |
| `holiday-week-checklist.pdf` | A day-by-day holiday-week checklist that schedules rest and deep breaths too. |
| `cards-you-owe-tracker.pdf` | Cards-you-owe tracker (picked / written / sent) plus an addresses-at-a-glance page. |

Every PDF starts with a warm "how to use it" page, then the sheet itself.

## Building the PDFs

One script builds every sheet from `src/*.html` + `src/base.css` using
[WeasyPrint](https://weasyprint.org/):

```bash
pip install -r requirements.txt   # weasyprint, pypdf, pytest
python3 build.py                  # renders all sheets into printables/
```

Options:

```bash
python3 build.py --out somedir            # build somewhere else
python3 build.py --only kids-wish-list    # build selected sheets (file stems)
```

The build is fully local: no network requests, no web fonts, no images.
PDFs are US Letter — print at 100% ("Actual size"), portrait.

## Running the tests

```bash
python3 -m pytest
```

The suite builds every sheet from source into a temp directory and verifies
that each one produces a valid PDF with a usage page, correct title metadata,
and no branding anywhere in the text.

## Editing a sheet

Sources are plain HTML in `src/`, sharing `src/base.css`. Change the words or
rows you like, run `python3 build.py`, and the PDFs regenerate. The list of
sheets in `build.py` (`SHEETS`) is the single source of truth for what gets
built and in what order.

## License & credits

Released under the MIT License — see [LICENSE](LICENSE).
Copyright (c) 2026 Asdale Dynamics, LLC.

Built with care by **Asdale Dynamics, LLC** — beginner-friendly AI guides,
books, and practical tools from Dylan Asdale (*The Massive AI Manual*), at
[dylanasdale.github.io](https://dylanasdale.github.io).
