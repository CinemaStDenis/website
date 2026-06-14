# Tasks — Cinéma Saint-Denis rebuild

Working backlog for the website redesign + programme automation. Checkboxes track
progress; see `specs/spec-questions.md` for the open questions that still gate
some of these, and `design-notes.md` for the design direction.

_Last updated: 2026-06-14_

---

## ⚠️ Housekeeping / handover — don't forget

- [x] **Migrated off Lewis's personal GitHub account.**
      The repo now lives at **`CinemaStDenis/website`** (the cinema's own org); it
      started at `lewis-smith/cinema-st-dennis` purely to get things moving.
  - [x] Create the cinema's own GitHub organisation (or shared volunteer account).
  - [x] Move the code to the cinema's org (new repo `CinemaStDenis/website`; `origin` repointed and `main` pushed 2026-06-14).
  - [ ] **Make the `CinemaStDenis/website` repo private.** ⚠️ Currently PUBLIC. Blocked: `lewis-smith` only has _write_ access, not admin — an org owner must change visibility (repo Settings → General → Danger Zone), or grant `lewis-smith` admin so this can be automated.
  - [ ] Re-point the **Cloudflare Pages** Git connection, deploy hooks and tokens at the new owner (when Cloudflare is set up).
  - [ ] Confirm the new owner controls the domain, TMDB key and social tokens too.
  - [ ] Archive / delete the old `lewis-smith/cinema-st-dennis` copy once everything's verified.

---

## Decisions locked so far

- Stack: **Hugo** (static + structured content) → source on **GitHub** → build/host on **Cloudflare Pages** (+ **R2** for posters, **Workers/Cron** for glue).
- Programme update = a **Claude skill**, run by a volunteer when each (monthly) programme is issued; must be **runnable from Claude Code on the web**.
- Automation can run **fully automatic** (no human approval step) — needs solid failure alerting as a result.
- Ticketing: **ticketingcine.com** (EMS1065); look up per-film IDs to deep-link "Réserver".
- Images/trailers: **TMDB-first** (AlloCiné only as fragile fallback).
- Cadence: the cinema issues a **monthly** programme (Word doc, ~4–5 weeks of films); the website **homepage shows the current week's** films, kept fresh by the scheduled rebuild.

---

## Phase 0 — Foundations

- [x] Three homepage design directions as mockups (`designs/`).
- [x] Local git repo + tailored `.gitignore` + README, pushed to GitHub.
- [ ] Run `claude init` to generate a `CLAUDE.md` so Claude Code has project context.
- [ ] Write `docs/specs/Architecture.md` (topology, data flow, decisions, what's still open).
- [x] Obtain a **real sample of the monthly Word document** — stored at `docs/samples/` (unblocks most parsing work).
- [ ] Close remaining spec questions (B, C, D, E, F2, F4) in `specs/spec-questions.md`.
- [ ] Pick which of the three designs to build (or a hybrid).

## Phase 1 — Website (Hugo)

- [ ] Scaffold Hugo project (config, CSS pipeline, base layout) — French (`fr`).
- [ ] Content model: `films` (page bundles), a `schedule` data file (the month's screenings; site surfaces the current week), `events`, and static pages (histoire, tarifs, accès/parking, bar).
- [ ] Port the chosen design into a Hugo theme (partials + layouts).
- [ ] Write the practical-info content (tarifs, accès, parking, bar, histoire).
- [ ] Cloudflare Pages: connect repo, pin `HUGO_VERSION`, custom domain + SSL, deploy previews.
- [ ] R2 bucket for posters + delivery wiring.
- [ ] Daily scheduled rebuild (Cloudflare Cron → deploy hook) so "aujourd'hui / cette semaine" stay correct.
- [ ] (Optional) Client-side search via Pagefind.

## Phase 2 — Programme automation (Claude skill)

- [ ] Define/lock the monthly programme input format (from the sample doc — see `docs/samples/`).
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

## To Process/Inbox

There should be an option to include a "special screening" on the homepage, which would be something like someone involved in the movie is coming to watch.

There are also routine special events which shoudl be present on the home page. Ciné classique and ciné rencontre du mecredi. these will be highlighted in the word document
