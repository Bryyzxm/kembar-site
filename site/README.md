# kembar — landing page

Static page for `kembar`, two locales (English at `/`, Indonesian at `/id/`), with a waitlist form.
No build step, no framework, no server. Open `index.html` directly or serve the folder.

Contract: `docs/SPEC.md`. It is a copy; the working copy lives with the product.
Brand assets and rules: `brand/README.md`.

## Files

```
site/
  index.html        English page
  id/index.html     Indonesian page
  assets/styles.css shared styles
  assets/hero-bg.jpg      one real frame, upscaled and blurred: the hero backdrop
  assets/*.jpg      real frames, resized copies of docs/screens/
  assets/mark.svg         brand mark on the sky tile
  assets/lockup-dark.svg  header lockup (mark + wordmark)
  assets/lockup-light.svg for light surfaces
  assets/favicon.svg      browser tab
  _headers          Cloudflare Pages cache and security headers
```

## The hero

Full-bleed backdrop, floating nav pill, headline bottom left, a glass card on the right, and a facts
rail along the bottom.

- `assets/hero-bg.jpg` is a 720 px, 62 KB crop of one real frame from `docs/screens/`. It is blurred
  18 px and scaled 1.16, so the resolution does not matter but the bytes do: it is the largest
  paint on the page. Regenerate with
  `sips -c 360 270 --cropOffset 0 0 docs/screens/after-talking-head.jpg --out /tmp/f1.jpg` then
  `sips --resampleWidth 720 -s formatOptions 38 /tmp/f1.jpg --out site/assets/hero-bg.jpg`.
- The glass card lists the six things a style is measured on. It shows no numbers, because no
  measured numbers exist yet and inventing them would break the rule that proof is real.
- The Indonesian headline gets a smaller size through `html[lang="id"] .hero h1`. Indonesian runs
  about a fifth longer than English and at the English size it broke into four lines.
- Below 860 px the glass card hides and below 560 px the facts rail hides. Both restate content from
  "how it works" and "what exists today", and on a phone they pushed the before/after proof past the
  first screen. Measured at 375 × 812: the Before strip sits at 577 px and the After at 663 px, both
  above the fold.

Brand files are copies of `brand/`. Change the master, then copy.

## Palette

| Token | Hex | Use |
|---|---|---|
| `--ink` | `#071A24` | Page background |
| `--ink-2` | `#0C2431` | Cards and panels |
| `--paper` | `#FCFFFF` | Text |
| `--muted` | `#93AEB9` | Secondary text, 7.6:1 on ink |
| `--sky` | `#0593C6` | Eyebrows, links, focus, the emphasised word |
| `--pink` | `#D83995` | The After chip only |
| `--pink-ink` | `#150008` | Text on pink, 5.2:1 |
| `--media` | `#04121A` | Letterbox behind video frames |

Contrast on `--ink`: sky 5.16:1, pink 4.51:1, muted 7.6:1. Pink sits at the limit, so it carries
no small text — only the chip, whose text uses `--pink-ink`.

## Before this goes live

1. **Connect the waitlist.** Create a Buttondown account, then replace `YOUR-BUTTONDOWN-USERNAME`
   in `site/index.html` and `site/id/index.html` (the form `action` and its `data-connect`
   attribute). Until it is replaced the form refuses to submit and says so, on purpose — a waitlist
   that silently loses signups is worse than one that is visibly off.
2. **Deploy.** Cloudflare Pages → connect the repo → root directory `site` → no build command,
   output directory `.` (or drag the `site` folder into a direct upload).
3. **Add the domain**, then add these to both pages with fully qualified URLs — Google ignores
   relative `hreflang` and the audit fails because of it:

   ```html
   <link rel="canonical" href="https://DOMAIN/">
   <link rel="alternate" hreflang="en" href="https://DOMAIN/">
   <link rel="alternate" hreflang="id" href="https://DOMAIN/id/">
   ```

   Use `https://DOMAIN/id/` as canonical on the Indonesian page.
4. **UTM tags.** Every signup is tagged. The hidden `tag` field is filled from `?utm_source=` on
   load, so `domain.com/?utm_source=tiktok` lands as `utm:tiktok` in Buttondown. Without a UTM the
   tag falls back to the referrer host, then `direct`.

## Regenerating the image copies

Images are resized from `docs/screens/` with `sips`. They are copies — replacing a screenshot in
`docs/screens/` does not update the page.

```
sips -Z 1240 -s formatOptions 52 docs/screens/before-talking-head.jpg --out site/assets/before-talking-head.jpg
sips -Z 720  -s formatOptions 50 docs/screens/before-talking-head.jpg --out site/assets/before-talking-head-sm.jpg
sips -Z 1240 -s formatOptions 52 docs/screens/after-talking-head.jpg  --out site/assets/after-talking-head.jpg
sips -Z 720  -s formatOptions 50 docs/screens/after-talking-head.jpg  --out site/assets/after-talking-head-sm.jpg
sips -Z 820  -s formatOptions 68 docs/screens/after-product-video-1.jpg --out site/assets/product-video.jpg
sips -Z 820  -s formatOptions 68 docs/screens/after-teardown.jpg       --out site/assets/teardown.jpg
```

## How the languages work

`/` is English and carries a small script: if the browser's first language is Indonesian and the
visitor has never chosen a language, it sends them to `/id/`. `/id/` never redirects — so it stays
linkable and indexable — and the `English` / `Bahasa Indonesia` links write a `kembar_lang` cookie
that stops the redirect from overriding a deliberate choice.

## Measured

Lighthouse 12, this folder served on `localhost`, 2026-11-13, after the rebrand. Performance moves
a point between runs on an idle machine; everything else is stable.

| | Performance | Accessibility | Best practices | SEO |
|---|---|---|---|---|
| Mobile (`/`) | 98 | 100 | 100 | 100 |
| Mobile (`/id/`) | 97 | 100 | 100 | 100 |
| Desktop | 100 | 100 | 100 | 100 |

Mobile LCP 2.3 s (EN) and 2.6 s (ID), CLS 0, TBT 0 ms. No horizontal scroll at 375 px. The hero
backdrop is the largest paint, so its byte size sets these numbers.

Remaining flags are hosting-side and Cloudflare fixes them: text compression, long-lived asset
caching (see `_headers`), and next-gen image formats.
