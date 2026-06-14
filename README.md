# Cinéma Saint-Denis — site & automation

Redesign of the website for **Cinéma Saint-Denis**, a non-profit, volunteer-run
independent cinema in the Croix-Rousse (Lyon 4ᵉ). The site should convey the
flavour of the historic cinema, show the coming week's programme, and surface the
practical essentials — access, tarifs, parking, and the volunteer bar. In French.

## Status

Early planning and design exploration.

## Repo layout

- **`designs/`** — three homepage design directions as self-contained static
  mockups, plus a preview gallery (`index.html`):
  - `1-patrimoine.html` — heritage-led, editorial
  - `2-programme.html` — programme-first, showtime grid (Drafthouse-style)
  - `3-salon.html` — refined community hub (Comœdia-style)
  - `assets/logo.png` — original logo; brand garnet `#9C0000` was sampled from it
- **`docs/`** — planning & design documents:
  - `specs/design-brief.md`, `specs/technical-requirements.md`, `specs/spec-questions.md`
  - `design-notes.md`

## Planned stack

Hugo (static output with a structured content layer) · source on **GitHub** ·
build + host on **Cloudflare Pages**, with **R2** for posters and **Workers/Cron**
for the dynamic glue (forms, daily rebuild, calendar). A **Claude skill** parses
the weekly programme document, fetches posters/trailers (TMDB), updates the site,
generates a subscribable calendar, and posts to social.

## Preview the mockups

Open `designs/index.html` in a browser.
