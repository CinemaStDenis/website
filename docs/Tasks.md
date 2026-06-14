# Tasks — Cinéma Saint-Denis rebuild

Working backlog for the website redesign + weekly automation. Checkboxes track
progress; see `specs/Spec questions.md` for the open questions that still gate
some of these, and `Design notes.md` for the design direction.

_Last updated: 2026-06-14_

---

## ⚠️ Housekeeping / handover — don't forget

- [ ] **Migrate this project off Lewis's personal GitHub account.**
  The repo currently lives at **`lewis-smith/cinema-st-dennis`** (private, created
  2026-06-14) on a personal account purely to get things moving. Once the project
  progresses / before go-live, hand it over to the cinema and remove it from Lewis's account:
  - [ ] Create the cinema's own GitHub organisation (or shared volunteer account).
  - [ ] Transfer the repo to that owner (`gh repo transfer`, or Settings → Transfer ownership).
  - [ ] Re-point the **Cloudflare Pages** Git connection, deploy hooks and tokens at the new owner.
  - [ ] Confirm the new owner controls the domain, TMDB key and social tokens too.
  - [ ] Delete / archive the copy under `lewis-smith` once the transfer is verified.

---

## Decisions locked so far

- Stack: **Hugo** (static + structured content) → source on **GitHub** → build/host on **Cloudflare Pages** (+ **R2** for posters, **Workers/Cron** for glue).
- Weekly update = a **Claude skill**, run by a volunteer; must be **runnable from Claude Code on the web**.
- Automation can run **fully automatic** (no human approval step) — needs solid failure alerting as a result.
- Ticketing: **ticketingcine.com** (EMS1065); look up per-film IDs to deep-link "Réserver".
- Images/trailers: **TMDB-first** (AlloCiné only as fragile fallback).

---

## Phase 0 — Foundations

- [x] Three homepage design directions as mockups (`designs/`).
- [x] Local git repo + tailored `.gitignore` + README, pushed to GitHub.
- [ ] Write `docs/specs/Architecture.md` (topology, data flow, decisions, what's still open).
- [ ] Obtain a **real sample of the weekly Word document** (unblocks most parsing work).
- [ ] Close remaining spec questions (B, C, D, E, F2, F4) in `specs/Spec questions.md`.
- [ ] Pick which of the three designs to build (or a hybrid).

## Phase 1 — Website (Hugo)

- [ ] Scaffold Hugo project (config, CSS pipeline, base layout) — French (`fr`).
- [ ] Content model: `films` (page bundles), weekly `schedule` data file, `events`, and static pages (histoire, tarifs, accès/parking, bar).
- [ ] Port the chosen design into a Hugo theme (partials + layouts).
- [ ] Write the practical-info content (tarifs, accès, parking, bar, histoire).
- [ ] Cloudflare Pages: connect repo, pin `HUGO_VERSION`, custom domain + SSL, deploy previews.
- [ ] R2 bucket for posters + delivery wiring.
- [ ] Daily scheduled rebuild (Cloudflare Cron → deploy hook) so "aujourd'hui / cette semaine" stay correct.
- [ ] (Optional) Client-side search via Pagefind.

## Phase 2 — Weekly automation (Claude skill)

- [ ] Define/lock the weekly programme input format (from the sample doc).
- [ ] Parse the doc → structured screenings + film metadata.
- [ ] TMDB matching → poster / backdrop / trailer; handle no-match + manual override.
- [ ] ticketingcine.com: resolve per-film ticket IDs → booking deep links.
- [ ] Write Hugo content/data, push posters to R2, commit → triggers Cloudflare build.
- [ ] Failure alerting (email/Slack) since runs are unattended.
- [ ] Document how to run the skill from **Claude Code on the web** (step-by-step for volunteers).

## Phase 3 — Subscribable calendar

- [ ] Generate ICS feed(s) from schedule data (Hugo custom output format).
- [ ] Decide one feed vs. several (programme / ciné-club / jeune public).

## Phase 4 — Social media

- [ ] Confirm platforms (Facebook + Instagram? others) and posting model (Meta API vs scheduler vs drafts).
- [ ] Auto-post new films incl. trailer, on an agreed cadence.
- [ ] Caption generation/template (reuse blurb vs generate).

---

## Nice-to-have / later

- [ ] Newsletter integration (Brevo/Mailchimp + Cloudflare Worker form handler + Turnstile).
- [ ] Cloudflare Email Routing for `contact@cinema-saint-denis.fr`.
- [ ] Privacy-friendly analytics (Cloudflare Web Analytics — cookieless, no consent banner).
- [ ] Git-based CMS (Sveltia/Decap) for volunteers to edit non-automated pages.
- [ ] Migrate existing blog / "Notre histoire" / partners content from the old WordPress site.
