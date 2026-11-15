# kembar landing page

Static page for `kembar`, the hosted editor, two locales (English at `/`, Indonesian at `/id/`),
with an early-access form. No build step, no framework, no server.

Contract: `../_bmad-output/specs/spec-landing-page-waitlist/SPEC.md`.
Brand assets and rules: `../brand/README.md`.

## What the page says

The page sells one product, not a repository:

- **Product.** One long take in. It removes the retakes, captions one word at a time, and puts the
  real page on screen at the word that names it.
- **Buyer.** Solo talking-head creators who post weekly and already pay for something.
- **Status.** Early access, opened in small groups. No price is shown and there is no checkout, so
  the page cannot promise either.
- **No open-source copy.** There is no mention of a local install, a licence, a terminal or a
  coding agent. Those belong to the repository's README, not this page.

The trust section answers the seven complaints the market research found (credits burned by a
failed render, a watermark at export, a duration cap, a style forced with no off switch). It does so
as four policy statements. Keeping those four true is a product decision, not a copy decision.

## Files

```
site/
  index.html             English page
  id/index.html          Indonesian page
  assets/styles.css      shared styles
  assets/hero.mp4        the product shot: 12.7 s of a real edit, 640x1138
  assets/hero.jpg        the poster: the first frame of that video
  assets/proof-before.jpg    8 frames of the raw take, 1240x276
  assets/proof-before-sm.jpg same at 720 px wide
  assets/proof-after.jpg     8 frames of the same take after the edit
  assets/proof-after-sm.jpg  same at 720 px wide
  assets/card-page.jpg       the captured page, with the line marked
  assets/card-motion.jpg     a diagram card built for one sentence
  assets/card-counter.jpg    a logo with a counter climbing to the number
  assets/og.jpg              1200x630 share card
  assets/mark.svg        brand mark on the sky tile
  assets/lockup-dark.svg header lockup (mark + wordmark)
  assets/lockup-light.svg for light surfaces
  assets/favicon.svg     browser tab
  _headers               Cloudflare Pages cache and security headers
```

Brand files are copies of `brand/`. Change the master, then copy.

## Where the images come from

Every proof frame is a frame from one real edit made by the editor:

`/Users/bryyzxm/video_edit/edits/video-20261115-110838-2`

The edit is a 50/50 split, 9:16, 34 seconds, rendered from `render-normalized.mp4`. The take it came
from is `.source-cfr.mp4` in the same folder. Nothing on the page is a mockup, a stock frame or a
generated screenshot, and the two strips are the same take before and after.

Regenerate with `ffmpeg` (the frame times are chosen for the card each one shows):

```
E=/Users/bryyzxm/video_edit/edits/video-20261115-110838-2

# the hero video: five moments, hard cut, no audio, 640x1138, about 950 KB
ffmpeg -i $E/render-normalized.mp4 -filter_complex "\
[0:v]trim=14.9:18.2,setpts=PTS-STARTPTS,scale=640:-2,fps=30[a];\
[0:v]trim=0.9:4.2,setpts=PTS-STARTPTS,scale=640:-2,fps=30[b];\
[0:v]trim=7.9:9.6,setpts=PTS-STARTPTS,scale=640:-2,fps=30[c];\
[0:v]trim=22.2:24.6,setpts=PTS-STARTPTS,scale=640:-2,fps=30[d];\
[0:v]trim=29.6:31.6,setpts=PTS-STARTPTS,scale=640:-2,fps=30[e];\
[a][b][c][d][e]concat=n=5:v=1:a=0[out]" -map "[out]" \
  -c:v libx264 -profile:v main -pix_fmt yuv420p -crf 30 -preset slow -movflags +faststart -an hero.mp4

# the poster is the first frame of that video, so playback starts without a jump
ffmpeg -i hero.mp4 -frames:v 1 -q:v 5 hero.jpg

# share card
ffmpeg -ss 14.9 -i $E/render-normalized.mp4 -frames:v 1 \
  -vf "crop=1080:567:0:60,scale=1200:630" -q:v 4 og.jpg
ffmpeg -ss 14.9 -i $E/render-normalized.mp4 -frames:v 1 \
  -vf "crop=1080:567:0:60,scale=1200:630" -q:v 4 og.jpg

# the three cards
ffmpeg -ss 3.0  -i $E/render-normalized.mp4 -frames:v 1 -vf "crop=1080:675:0:60" -q:v 3 card-page.jpg
ffmpeg -ss 14.9 -i $E/render-normalized.mp4 -frames:v 1 -vf "crop=1080:675:0:60" -q:v 3 card-motion.jpg
ffmpeg -ss 30.1 -i $E/render-normalized.mp4 -frames:v 1 -vf "crop=1080:675:0:60" -q:v 3 card-counter.jpg

# the two strips: 8 frames each, 155x276, tiled to 1240x276
for t in 2 9 16 23 30 37 44 51; do ffmpeg -ss $t -i $E/.source-cfr.mp4 -frames:v 1 -q:v 2 "src/%02d.jpg"; done
for t in 1.0 4.2 8.6 11.9 14.9 18.6 23.3 30.0; do ffmpeg -ss $t -i $E/render-normalized.mp4 -frames:v 1 -q:v 2 "ren/%02d.jpg"; done
ffmpeg -framerate 1 -i src/%02d.jpg -vf "scale=155:276,tile=8x1" -frames:v 1 -q:v 4 proof-before.jpg
ffmpeg -framerate 1 -i ren/%02d.jpg -vf "scale=155:276,tile=8x1" -frames:v 1 -q:v 4 proof-after.jpg
sips -Z 720 -s formatOptions 46 proof-before.jpg --out proof-before-sm.jpg
sips -Z 720 -s formatOptions 46 proof-after.jpg  --out proof-after-sm.jpg
```

The loop above overwrites `src/01.jpg` every time as written; give each iteration its own filename
(the shipped files were made with a counter).

## The hero

Dark ink, headline on the left, one real 9:16 edit on the right, four facts along the bottom.

- The right column is a muted, looping `assets/hero.mp4` (12.7 s, 640x1138, 947 KB) with
  `assets/hero.jpg` as its poster. The poster is the first frame of the video, so there is no jump
  when playback starts.
- The poster is still the largest paint and sets the mobile LCP. Keep it under 50 KB.
- Autoplay is muted and looping, which WCAG 2.2.2 allows only with a pause control, so there is one:
  a 38 px button over the bottom-right corner that swaps between pause and play icons and updates its
  accessible label. Under `prefers-reduced-motion: reduce` the video never starts and the button
  reads Play.
- The player also pauses itself when the hero scrolls out of view and resumes when it comes back,
  unless the visitor paused it themselves.
- No audio track ships, so nothing plays sound without a gesture.
- The four facts carry the wedge rather than a licence: the real page, one word per caption, your
  approval, and a switch on every automatic choice.
- Below 860 px the shot sits under the copy at 300 px. Below 560 px it hides, and so does the facts
  rail: both repeat what the proof strips and the sections say, and on a phone they pushed the strips
  past the first screen. Measured at 375 × 812: the take strip starts at 540 px and the edit strip at
  623 px, both above the fold. The player checks `offsetParent` before it calls `play()`, so a hidden
  hero does not download the video on a phone.
- The hero has no background photograph. The old one was a blurred frame behind a dark scrim; with a
  real frame in the layout it only competed with the proof.

## Palette

| Token | Hex | Use |
|---|---|---|
| `--ink` | `#071A24` | Page background |
| `--ink-2` | `#0C2431` | Cards and panels |
| `--paper` | `#FCFFFF` | Text |
| `--muted` | `#93AEB9` | Secondary text, 7.6:1 on ink |
| `--sky` | `#0593C6` | Eyebrows, links, focus, the emphasised word |
| `--pink` | `#D83995` | The edit chip only |
| `--pink-ink` | `#150008` | Text on pink, 5.2:1 |
| `--media` | `#04121A` | Letterbox behind the frames |

Contrast on `--ink`: sky 5.16:1, pink 4.51:1, muted 7.6:1. Pink sits at the limit, so it carries
no small text, only the chip, whose text uses `--pink-ink`.

## Deploy

The page is a Cloudflare **Worker** named `kembar`, connected to `Bryyzxm/kembar-site`, serving
`site/` as static assets at `https://kembar.web.id`. Push to `main` and the Worker builds; `_headers`
is read from this folder.

Still open:

- **`http://` does not redirect to `https://`.** Turn on Always Use HTTPS in SSL/TLS, Edge Certificates.
- **`www.kembar.web.id` does not resolve.** Add it as a second custom domain on the Worker, then a
  301 redirect rule from `www` to the apex.
- **The early-access list is wired but unproven.** Submit an address on the live page and confirm the
  Buttondown email arrives.

The form posts to `https://buttondown.com/api/emails/embed-subscribe/bryyzxm` in both pages, with
`data-connect` set to the same username. Replace both if the account changes. Never point it at
`buttondown.email`: Indonesian ISP DNS resolves that domain to the Kominfo block page, so the form
fails silently for local visitors. Until it is set the form refuses to submit and says so, on
purpose: a list that silently loses signups is worse than one that is visibly off.

**UTM tags.** Every signup is tagged. The hidden `tag` field is filled from `?utm_source=` on load,
so `kembar.web.id/?utm_source=tiktok` lands as `utm:tiktok` in Buttondown. Without a UTM the tag
falls back to the referrer host, then `direct`.

Canonical, `hreflang`, `og:url`, `og:image`, `sitemap.xml` and `robots.txt` all use
`https://kembar.web.id`.

## How the languages work

`/` is English and carries a small script: if the browser's first language is Indonesian and the
visitor has never chosen a language, it sends them to `/id/`. `/id/` never redirects, so it stays
linkable and indexable, and the `English` / `Bahasa Indonesia` links write a `kembar_lang` cookie
that stops the redirect from overriding a deliberate choice.

## Measured

Not re-measured since the page was rewritten on 2026-11-15. The version before it, on the same
Worker and `_headers`, measured Lighthouse 12 against the live site at 97/100/100/100 on mobile
English, 99/100/100/100 on mobile Indonesian and 100s on desktop, with mobile LCP 2.6 s and 1.8 s.
Re-run against the live domain before announcing.

Weights now: poster 44 KB and the two strips at 20 KB each above the fold, CSS and SVG 13 KB, the
947 KB video streaming behind the poster, and 124 KB of cards deferred below it. The video is the
one addition that could move a performance score, so measure once with it playing and once paused.
