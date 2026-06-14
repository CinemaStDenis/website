# Spec questions — automation pipeline

> Open questions to resolve before writing the detailed spec for the programme
> automation described in `technical-requirements.md` (parse the monthly Word doc
> → update the website → fetch images/trailers → publish a subscribable calendar
> → post to social media).
>
> **How to use:** answer inline under each `Réponse :` line. Where a
> **Recommended default** is given, you can often just reply "ok" / "confirmed"
> or correct it. The single most useful thing you can attach is **one real
> example of the monthly Word document** — it answers much of section B on its own.

_Created: 2026-06-14 · Updated: 2026-06-14 · Status: in progress — sample doc received; section B + A2 answered from it_

---

## A. Foundational decisions (these shape everything else)

**A1. Website platform — keep WordPress or rebuild?**
"Update the website" means very different things depending on this.
_Recommended default:_ static site + lightweight headless content (cheap/free
hosting, fast, secure, low-maintenance) for a volunteer-run non-profit.

The core loop:

1. Hugo source (content, templates, config) lives in a GitHub repo.
2. Cloudflare Pages connects to that repo via the Cloudflare GitHub App.
3. Push to main → Pages pulls the repo, runs hugo in its build container, deploys the static output to Cloudflare's edge CDN. PRs/branches get their own
   preview URLs automatically.
4. Custom domain + automatic SSL on Pages, free.

> **Réponse :**

**A2. Where do showtimes actually come from?**
Does the Word doc contain the full schedule (film × day × time), or only the
editorial blurb, with times living elsewhere (ticketing system / spreadsheet)?
This is the crux — site, calendar and social all derive from the schedule.

> **Réponse :**

The Word doc contains the **full schedule**. Each film block has a showtimes line
with date + time per screening, e.g. "Je 11/6 (20h30), Ve 12/6 (14h30), Sa 13/6
(20h30), Di 14/6 (17h)". So site, calendar and social can all be derived from the
doc — no separate showtimes source needed (ticketingcine stays the booking
target). Parser notes: French day abbreviations (Je/Ve/Sa/Di/Lu/Ma/Me) and mixed
time formats (`20h30`, bare `17`) need normalising; a film's screenings can span
several weeks of the month.

**A3. Do you sell tickets online today, and through what?**
(Mapado, BilletWeb, Ciné Office, etc.) The "Réserver" button needs a target,
and that system may be the real source of truth for screenings.

> **Réponse :**

Tickets are sold from: https://www.ticketingcine.com/?EMS1065#home
As part of the process, it would be good to look up the ids for the movies on there so we can link directly to ticket purchase for that movie.

**A4. Human-in-the-loop or fully autonomous?**
Should volunteers review/approve before site/calendar/social go live, or hands-off?
_Recommended default:_ review-before-publish, at least for social.

> **Réponse :**

A preview should be generated and approved before publish.

**A5. What is "a skill", and who runs it?**
A Claude skill a volunteer runs each month (drop doc → run → review → publish),
or a scheduled server job with no human? And how technical are the operators?

> **Réponse :**

## A claude skill, run by one of the volunteers.

## B. The monthly Word document (the input)

**B1. Is the format fixed, or can we define the template?**
A consistent template (or shared Google Sheet/Form) makes parsing far more
robust than free-form Word. Who produces it, and is the structure stable month to month?

> **Réponse :**

Free-form Word (`.docm`, the "version imprimeur" / print layout), issued monthly.
Not a rigid template, but the per-film structure is consistent and parseable —
see the real sample at `docs/samples/`. Worth confirming who produces it and
whether we can lightly standardise it to make parsing more robust.

**B2. What fields does it contain per film?**
Title, director, country, duration, version (VF/VOST), synopsis, showtimes?
Tables or prose? `.docx`? Any embedded images?

> **Réponse :**

Prose, no tables. Per film: TITLE (caps) · `de DIRECTOR` · `(country / year /
duration / VO if subtitled)` · `Avec CAST` · a showtimes line · synopsis · one or
more press quotes with the source in parentheses. Format is `.docm`. **No embedded
images** — every poster/still must come from TMDB. Some films carry a one-line
banner above the title (e.g. "Nouvelle et dernière séance", "Un grand classique
du rire").

**B3. How are films identified for matching to TMDB/AlloCiné?**
French title only, or also original title / year / director? Title-only matching
is error-prone (remakes, common titles); one disambiguating field per film helps a lot.

> **Réponse :**

The doc gives French title + director + country + year + duration for every film.
Director + year are strong disambiguators — match on title, then verify against
director/year/runtime to avoid remakes and common-title collisions.

**B4. Does the same doc cover special programming?**
Ciné-club, jeune public, séances scolaires, Q&As, festivals — same doc or separate?

> **Réponse :**

Yes — same doc. The sample mixes in: an outdoor "Ciné Rencontre du mercredi"
(surprise film + buvette), "Fête du Cinéma" pricing days (28–30 June, 5€), a
repertory classic (Tati, 1953, "avec présentation"), one-off "nouvelle/dernière
séance" notes, and a summer-closure notice (réouverture 3 septembre). This matches
the inbox note that Ciné classique / Ciné rencontre are highlighted in the doc —
so the parser must handle non-film events and special pricing, not just standard
screenings.

**B5. How are mid-week changes handled?**
Cancellations / time changes: re-run the whole doc, or edit in place?

> **Réponse :**

This is not a concern.

---

## C. Images & trailers

**C1. TMDB-first?**
Heads-up: AlloCiné has **no official public API** — using it means scraping
(fragile, legally grey). TMDB has a clean, free API.
_Recommended default:_ TMDB primary, manual override fallback; AlloCiné nice-to-have only.

> **Réponse :**

Confirmed — TMDB-first, with a manual-override fallback (AlloCiné nice-to-have
only). Especially important now we know the doc carries **no images at all**:
posters, backdrops and trailers all come from TMDB.

**C2. What assets do you want pulled?**
French poster only, or also backdrops/stills? Trailers (from TMDB's YouTube
links) — VO or VF preferred?

> **Réponse :**

Doc has no images, so all visuals come from TMDB. Pull the posters to use on the website and the backdrop images and trailer links to use elsewhere.

**C3. Any concern about image rights?**
TMDB posters are generally fine for editorial/promo use — please confirm you're comfortable.

> **Réponse :**

This is not a concern.

---

## D. The subscribable calendar

**D1. iCal/ICS feed?**
A subscribe-by-URL ICS feed works with Google, Apple and Outlook.
_Recommended default:_ yes, ICS feed(s). Confirm vs. a specific Google Calendar.

> **Réponse :**

it should be a google calendar which people can subscribe to

**D2. One calendar or several?**
e.g. main programme + ciné-club + jeune public as separate subscribable feeds.

> **Réponse :**

We only need one calendar

**D3. Event granularity?**
_Recommended default:_ one event per individual screening (film + date + time +
version + booking link). Agreed?

> **Réponse :**

One event per screening

---

## E. Social media

**E1. Which platforms?**
You have a Facebook page — also Instagram? X / Mastodon? A newsletter?

> **Réponse :**

Facebook & a brevo newsletter

**E2. Posting model — reality check.**
Facebook/Instagram via the Meta Graph API needs a Business app, expiring page
tokens and app review (non-trivial to set up and maintain). Alternatives:
(a) tool generates **draft posts a volunteer approves/publishes**, or
(b) tool feeds a scheduler (Buffer/Later). Which model?

> **Réponse :**

We have a business account for the cinema. But the skill should generate content that can be copied and pasted

**E3. Cadence & content?**
One post per new film, a weekly "what's on" roundup, or both? Poster + blurb +
showtimes + booking link + trailer? Reuse the doc's blurb as caption, or generate one?

> **Réponse :**

One post per film

---

## F. Operations

**F1. Hosting & budget?**
_Assumption:_ as close to free as possible → favours static hosting + a scheduled function.

> **Réponse :**

Repo on github and hosting on Cloudflare

**F2. Who owns / can grant access** to the domain, hosting, TMDB account and social accounts?

> **Réponse :**

Audrey will own it in an account named for the cinema

**F3. Who maintains this long-term?**
Volunteer turnover means it must be low-maintenance and well-documented
(another argument for TMDB-over-AlloCiné and approve-before-post).

> **Réponse :**

Part of the spec should be to document how to run the skill from claude code online.

The plan is for Audrey to run this.

**F4. Priorities / MVP & any deadline?**
_Recommended sequencing:_ (1) new site + programme-from-doc → (2) calendar feed
→ (3) social. Does that order match yours?

> **Réponse :**

Sounds good

---

## G. Ticketing & Publishing

**G1. What vendor is used for online ticketing?**

> **Réponse :**

https://www.ticketingcine.com/?EMS1065#home

**G2. Who updates the ticketing system?**

> **Réponse :**

It's done manually by another volunteer. If the system is looking for deeplinks on ticketingcine but can't find them it can just link to the root.

**G3. Does the system have a link to Allo Ciné? **

Yes, via the ticketing system

> **Réponse :**

## Most valuable next input

📎 **One real example of the monthly Word document.** It would resolve most of
section B (and how parsing/matching must work) in one go.

> **Attached / location :** ✅ Received — `docs/samples/programme-juin-juillet-2026.docm`
> (real monthly programme, juin–juillet 2026; plain-text extraction alongside as
> `.txt`). Section B and A2 above are answered from it.
