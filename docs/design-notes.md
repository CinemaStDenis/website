# Cinéma Saint-Denis — Notes de conception (Design notes)

> Living design document for the website redesign. Captures an audit of the
> current site, the brand assets, reference sites, the real content inventory,
> and the three homepage concepts. Update as decisions are made.

_Last updated: 2026-06-14_

---

## 1. Brief, in one line

Redesign the homepage for **Cinéma Saint-Denis** — a non-profit, volunteer-run
independent cinema in the Croix-Rousse (Lyon 4e) — so it conveys the *flavour of
the historic cinema*, shows the *coming week's programme*, and makes the
practical essentials (location, pricing, parking, concessions) easy to find.
**In French.** Keep the existing colours and logo.

---

## 2. Current site audit — `cinema-saint-denis.fr`

A WordPress site (uploads under `/wp-content/`, 2022 theme). Functional but
dated; reads as a community noticeboard rather than a destination.

**Navigation:** Programme · Infos Pratiques · Notre histoire · Blog
Submenus: Films du mois · Courts-métrages · Tarifs · Séances scolaires

**Homepage sections (today):**
1. Welcome / cinema overview
2. "100 ans d'histoire" highlight
3. Current films (4 titles, week of 11–16 June 2026)
4. Partner organisations
5. Contact / location
6. Newsletter sign-up

**Self-description (tone to preserve):**
- « Convivial et accueillant, avec des tarifs pour toutes les bourses »
- « un cinéma de proximité »

**What works:** warm, community voice; clear non-profit identity; the
century-old heritage is a genuine asset.
**What to improve:** showtimes aren't visible on the homepage; practical info
(parking, bar, hours) is buried; little visual atmosphere; no clear hierarchy or
call to action; not obviously the home of a *cinéma classé* with real character.

---

## 3. Brand assets

### Logo
- File: `cropped-LOGO_CINEMA_ST_DENIS_GRENAT-e1658649229651.png`
- Saved locally at `designs/assets/logo.png` (510 × 261, transparent PNG).
- A single-colour **garnet** wordmark ("grenat" = garnet in the filename).
- For dark backgrounds, render the wordmark in cream/white
  (`filter: brightness(0) invert(1)`), keeping garnet for accents elsewhere.

### Colour — sampled directly from the logo
The dominant opaque pixel is **`#9C0000`** — `rgb(156, 0, 0)`. This is *the*
brand colour. Palette built around it:

| Token            | Hex       | Use                                            |
|------------------|-----------|------------------------------------------------|
| Garnet (brand)   | `#9C0000` | Primary — wordmark, headings, key accents      |
| Oxblood (deep)   | `#5E0A0A` | Depth, dark sections, hovers                   |
| Crimson (bright) | `#D11A1A` | CTAs / "Réserver" on dark backgrounds          |
| Brass / gold     | `#B08A3E` | Heritage accent, rules, marquee bulbs          |
| Parchment        | `#F5ECDB` | Warm light background (heritage)               |
| Ivory            | `#FBFAF7` | Clean light background (refined)               |
| Warm black       | `#16110F` | Dark background / ink                          |
| Ink              | `#20181A` | Body text on light                             |

### Typography direction
- **Heritage:** Fraunces (display serif) + Spectral (body serif) — vintage, editorial.
- **Programme-first:** Oswald / heavy condensed caps + Inter (body) — bold, utilitarian.
- **Refined:** Cormorant Garamond (display) + Inter/Mulish (body) — elegant, airy.

---

## 4. Reference sites — what we borrow

**Alamo Drafthouse (Downtown Brooklyn)** — bold, dark, confident. The signature
move is a dense, scannable **weekly showtime grid** with strong "Get Tickets"
CTAs. Programme-first; you always know what's on and can act immediately.
→ Feeds **Design 2**.

**Cinéma Comœdia (Lyon)** — refined, minimalist, lots of whitespace and neutral
tone. "À L'AFFICHE" / "PROCHAINEMENT", a downloadable programme, and — crucially
— a **bistro** and membership cards that frame the cinema as a *cultural
destination and community hub*, not a ticket counter.
→ Feeds **Design 3**.

Both are Lyon-adjacent arthouses, which is why they resonate.

---

## 5. Content inventory (single source of truth for mockups)

Real where known; **illustrative/placeholder where marked `‡` — confirm with the cinema.**

**Identity**
- Cinéma Saint-Denis — cinéma associatif (loi 1901), géré par des bénévoles.
- Croix-Rousse, Lyon. « Depuis 1920 »‡ (≈ 100 ans — confirm exact year).
- Tagline kept: « Convivial et accueillant — des tarifs pour toutes les bourses ».

**Programme — semaine du 11 au 17 juin 2026** (4 real titles; showtimes ‡)
| Film | Pays / durée | Version |
|------|--------------|---------|
| C'est quoi l'amour ? | France · 1h48 | VF |
| Mon grand frère et moi | Japon · 2h07 | VOST |
| Vivaldi et moi | Italie · 1h50 | VOST |
| Juste une illusion | France · 2h00 | VF |
Plus séances spéciales‡ : ciné-club, ciné-goûter, séance VO / rencontre.

**Lieu & accès**
- 77 grande rue de la Croix-Rousse, 69004 Lyon
- Métro C — arrêt Croix-Rousse (3 min)‡ ; Bus C13 / C18‡ ; Vélo'v à proximité‡
- Tél : 04 78 39 81 51 · contact@cinema-saint-denis.fr · facebook.com/CinemaSaintDenis

**Tarifs‡** (affordable arthouse — confirm all)
- Plein 7,50 € · Réduit 6,00 € · −14 ans 4,50 € · Adhérent 5,50 €
- Mardi, tarif unique 5,50 € · Carte 10 séances 55 € · Adhésion annuelle 12 €

**Parking‡**
- Parking LPA Croix-Rousse (≈ 5 min) · Voirie (gratuite dim. & après 19h)
- Quartier piéton — transports / vélo recommandés.

**Concessions / Bar associatif‡**
- Bar tenu par les bénévoles ; ouvre 1h avant et reste ouvert après les séances.
- Vins de producteurs, bières artisanales, cafés, douceurs ; prix doux.
- Recettes reversées au cinéma ; lieu d'échange après les films.

**Histoire / flavour**
- Salle unique « à l'italienne »‡, ≈ 250 fauteuils‡, classée‡.
- « De la lanterne magique au numérique » ; 100 % bénévole.

---

## 6. Requirements checklist (every concept must hit these)

- [x] Flavour of the historic cinema
- [x] Programme for the coming week
- [x] Location / access
- [x] Pricing
- [x] Parking
- [x] Concessions
- [x] French language
- [x] Original garnet colour + logo

---

## 7. The three homepage concepts

Three genuinely different *organising principles*, not three skins.

### Design 1 — « Le Patrimoine » (heritage-led, editorial)
Leads with story and atmosphere. Parchment + garnet + brass, vintage serif, an
art-deco marquee motif, programme presented as a "programme de la semaine"
playbill with ticket-stub showtimes. For visitors who fall in love with the
*place* first. File: `designs/1-patrimoine.html`.

### Design 2 — « Le Programme » (programme-first, Drafthouse-style)
Leads with what's on. Dark, bold, condensed caps; a featured film hero and the
signature **weekly showtime grid** (films × days) with prominent "Réserver"
CTAs. For visitors who came to book. File: `designs/2-programme.html`.

### Design 3 — « Le Salon » (refined community hub, Comœdia-style)
Balanced and airy. Ivory + a single garnet accent, elegant high-contrast serif,
generous whitespace. Foregrounds the **bar associatif** and the volunteer ethos
as a cultural-destination feature alongside a calm "À l'affiche" grid. For
visitors choosing where to spend an evening. File: `designs/3-salon.html`.

Preview gallery: `designs/index.html`.

---

## 8. Technical / future notes (from `technical-requirements.md`)

Out of scope for these mockups, but the design should anticipate:
- A **monthly** Word document of film blurbs → parsed to update the site (the
  homepage then shows the current week).
- Auto-fetch posters/stills from **TMDB / AlloCiné** (mockups use designed
  placeholders where posters will go).
- Publish a **subscribable calendar** (the showtime grid maps to this).
- Auto-post new films + trailers to **social media**.

---

## 9. Open questions — to confirm with the cinema

1. Exact founding year (« depuis 19?? ») and key heritage facts (seats, listing).
2. Real tarifs and any current offers (the mardi tariff, membership price).
3. Actual showtimes per film (mockups use plausible placeholders).
4. Photography — facade, auditorium, the bar, screenings (big quality lever).
5. Which of the three directions to develop — or a hybrid.
