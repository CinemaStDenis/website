# Sample programme documents

Real examples of the cinema's **monthly** programme — the Word document the
automation parses. Kept here as reference for building and testing the parser.

> The programme is **monthly**; the website homepage is refreshed **weekly** to
> show the current week's films.

## `programme-juin-juillet-2026.docm`

- **Source filename:** `Programme jui-juillet_version imprimeur.docm` (the
  print-shop / *version imprimeur* layout).
- **Covers:** 11 June → 7 July 2026 (~4 weeks), then summer closure
  (*réouverture jeudi 3 septembre*).
- **Format:** free-form Word (`.docm`), **text only — no embedded images**, so
  posters/stills must come from TMDB. One block per film:
  - `TITLE` (caps) · `de DIRECTOR` · `(country / year / duration / VO if subtitled)`
  - `Avec CAST`
  - a showtimes line — `Je 11/6 (20h30), Ve 12/6 (14h30), …`
  - synopsis, then press quotes with the source in parentheses
- Also carries **special programming** in the same doc: an outdoor *Ciné
  Rencontre du mercredi*, *Fête du Cinéma* pricing days (28–30 June, 5€), a
  repertory classic (Tati, with intro), *nouvelle/dernière séance* notes, and
  the summer-closure notice.
- The `.txt` alongside is a plain-text extraction (via `textutil`) for quick
  reading / diffing.
