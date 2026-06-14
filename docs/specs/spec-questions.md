# Spec questions — automation pipeline

> Open questions to resolve before writing the detailed spec for the weekly
> automation described in `technical-requirements.md` (parse the weekly Word doc
> → update the website → fetch images/trailers → publish a subscribable calendar
> → post to social media).
>
> **How to use:** answer inline under each `Réponse :` line. Where a
> **Recommended default** is given, you can often just reply "ok" / "confirmed"
> or correct it. The single most useful thing you can attach is **one real
> example of the weekly Word document** — it answers much of section B on its own.

_Created: 2026-06-14 · Status: awaiting answers_

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

It can be fully automatic

**A5. What is "a skill", and who runs it?**
A Claude skill a volunteer runs each week (drop doc → run → review → publish),
or a scheduled server job with no human? And how technical are the operators?

> **Réponse :**

## A claude skill, run by one of the volunteers.

## B. The weekly Word document (the input)

**B1. Is the format fixed, or can we define the template?**
A consistent template (or shared Google Sheet/Form) makes parsing far more
robust than free-form Word. Who produces it, and is the structure stable week to week?

> **Réponse :**

**B2. What fields does it contain per film?**
Title, director, country, duration, version (VF/VOST), synopsis, showtimes?
Tables or prose? `.docx`? Any embedded images?

> **Réponse :**

**B3. How are films identified for matching to TMDB/AlloCiné?**
French title only, or also original title / year / director? Title-only matching
is error-prone (remakes, common titles); one disambiguating field per film helps a lot.

> **Réponse :**

**B4. Does the same doc cover special programming?**
Ciné-club, jeune public, séances scolaires, Q&As, festivals — same doc or separate?

> **Réponse :**

**B5. How are mid-week changes handled?**
Cancellations / time changes: re-run the whole doc, or edit in place?

> **Réponse :**

---

## C. Images & trailers

**C1. TMDB-first?**
Heads-up: AlloCiné has **no official public API** — using it means scraping
(fragile, legally grey). TMDB has a clean, free API.
_Recommended default:_ TMDB primary, manual override fallback; AlloCiné nice-to-have only.

> **Réponse :**

**C2. What assets do you want pulled?**
French poster only, or also backdrops/stills? Trailers (from TMDB's YouTube
links) — VO or VF preferred?

> **Réponse :**

**C3. Any concern about image rights?**
TMDB posters are generally fine for editorial/promo use — please confirm you're comfortable.

> **Réponse :**

---

## D. The subscribable calendar

**D1. iCal/ICS feed?**
A subscribe-by-URL ICS feed works with Google, Apple and Outlook.
_Recommended default:_ yes, ICS feed(s). Confirm vs. a specific Google Calendar.

> **Réponse :**

**D2. One calendar or several?**
e.g. main programme + ciné-club + jeune public as separate subscribable feeds.

> **Réponse :**

**D3. Event granularity?**
_Recommended default:_ one event per individual screening (film + date + time +
version + booking link). Agreed?

> **Réponse :**

---

## E. Social media

**E1. Which platforms?**
You have a Facebook page — also Instagram? X / Mastodon? A newsletter?

> **Réponse :**

**E2. Posting model — reality check.**
Facebook/Instagram via the Meta Graph API needs a Business app, expiring page
tokens and app review (non-trivial to set up and maintain). Alternatives:
(a) tool generates **draft posts a volunteer approves/publishes**, or
(b) tool feeds a scheduler (Buffer/Later). Which model?

> **Réponse :**

**E3. Cadence & content?**
One post per new film, a weekly "what's on" roundup, or both? Poster + blurb +
showtimes + booking link + trailer? Reuse the doc's blurb as caption, or generate one?

> **Réponse :**

---

## F. Operations

**F1. Hosting & budget?**
_Assumption:_ as close to free as possible → favours static hosting + a scheduled function.

> **Réponse :**

I was thinking of keeping a repo on github and hosting on Cloudflare

**F2. Who owns / can grant access** to the domain, hosting, TMDB account and social accounts?

> **Réponse :**

**F3. Who maintains this long-term?**
Volunteer turnover means it must be low-maintenance and well-documented
(another argument for TMDB-over-AlloCiné and approve-before-post).

> **Réponse :**

Part of the spec should be to document how to run the skill from claude code online.

**F4. Priorities / MVP & any deadline?**
_Recommended sequencing:_ (1) new site + programme-from-doc → (2) calendar feed
→ (3) social. Does that order match yours?

> **Réponse :**

---

## G. Ticketing & Publishing

**G1. What vendor is used for online ticketing?**

> **Réponse :**

**G2. Who updates the ticketing system?**

> **Réponse :**

**G3. Does the system have a link to Allo Ciné? **

Yes, via the ticketing system

> **Réponse :**

## Most valuable next input

📎 **One real example of the weekly Word document.** It would resolve most of
section B (and how parsing/matching must work) in one go.

> **Attached / location :**
