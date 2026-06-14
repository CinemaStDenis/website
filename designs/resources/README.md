# Design Resources

Design reference material and source files — anything that informs the look and
feel but isn't a finished mockup or a production asset.

Suggested contents:

- **Brand** (`resources/brand/`) — colour palettes, typography specs, and
  *editable/source* logo artwork (vector originals, layered files, alternate
  lockups)
- **Fonts** — font files or licence notes
- **References** — inspiration, screenshots, moodboards
- **Source files** — Figma exports, Sketch/Affinity files, original artwork

## Where the logo lives

The **production logo is `designs/assets/logo.png`** — the single source of
truth that the mockups (and, later, the Hugo site) reference. The brand garnet
`#9C0000` was sampled from it.

Keep editable *source* artwork (vector, layered files, variants) in
`resources/brand/` if/when we have it, but the canonical exported logo stays in
`assets/`. **Don't copy the production PNG in here** — one home, no "which is
current?" confusion later.

> Finished HTML mockups live in `designs/`. Assets used directly by those
> mockups live in `designs/assets/`.
