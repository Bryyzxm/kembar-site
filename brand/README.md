# kembar — brand assets

Open `preview.html` in a browser to see every file on dark, light, sky and pink.

## The name

**kembar** — Indonesian for *twin*. Two versions of the same take: your video, and the one that
looks like you made it.

Lowercase. The period is part of the **wordmark** and belongs only there: the lockups and the page
title carry `kembar.`, while body copy writes `kembar` with no period, so it reads inside a
sentence. Do not type the wordmark by hand in a font — use the lockup files.

Tagline in English: **the edit that looks like you.** In Indonesian: **edit yang kelihatan kamu
yang bikin.**

## The mark

Two 16:9 frames, offset, the front one carrying a caption. The back frame is the version the editor
made; the front frame is the one you kept.

## Files

| File | Use |
|---|---|
| `mark.svg` | Primary mark on the sky tile. Works on any background. |
| `lockup-dark.svg` | Mark + white wordmark. Dark surfaces. |
| `lockup-light.svg` | Mark + ink wordmark. Light surfaces. |
| `favicon.svg` | Same geometry as `mark.svg`, no title, for the browser tab. |
| `avatar.svg` | 512 × 512 ink field with the mark at 62%. Social profile pictures. |
| `preview.html` | The brand sheet. |
| `explorations/` | The rejected variants, kept so the reasoning stays visible. |

## Palette

| | Hex | Use |
|---|---|---|
| Sky Blue | `#0593C6` | The tile, interactive accents, links, the emphasised word. 5.16:1 on Ink. |
| Hot Pink | `#D83995` | The second frame, the "after" highlight, emphasis. One per screen. 4.51:1 on Ink. |
| Pink ink | `#150008` | Text on pink. 5.2:1 — pink is too light to hold white or ink text safely. |
| White | `#FCFFFF` | Text on dark, the front frame. |
| Ink | `#071A24` | Background for dark surfaces, wordmark on light. |

Hot Pink is an accent, not a surface. If a layout has pink in three places, one of them is wrong.
Because it sits at 4.51:1 on Ink, never put small text in pink.

Do not put the tile version of the mark on a pink background — the back frame disappears into the
field. On pink, use the white lockup or drop the tile.

## Rules

- Minimum size for the tile mark: 16 px. Below that, use the raw frames without the tile.
- Clear space around the mark: half the tile height on all sides.
- Never recolour the frames to anything outside the palette, and never rebuild the mark with a
  different play glyph.
- The wordmark is outlined — it carries no font dependency. Do not retype it in a font.

## Typography

The wordmark is **Inter Bold** (`wght 700`, `opsz 32`), tracking −0.02 em, converted to outlines.
Inter is licensed under the SIL Open Font License, so the outlines are safe to ship. Body copy on
the site should use a system sans stack; Inter is optional for headlines.

## Not done yet

- A one-colour version for stamps, watermarks and single-colour print.
- PNG and ICO favicons for browsers that do not read SVG.
- App icons at platform-specific sizes.
