# kembar-site

The public page for kembar, and the waitlist form on it. Plain HTML and CSS, no build step, no
framework, no server.

| Path | What it is |
|---|---|
| `site/` | The deployable site. Cloudflare Pages output directory is `site`. |
| `brand/` | Mark, lockups, palette and the rules that govern them. |
| `docs/SPEC.md` | The contract the page is built against. A copy of the working document. |
| `deploy/` | How it gets published, including the is-a.dev record. |

Read `site/README.md` before editing the page, and `brand/README.md` before changing a colour or the
mark.

## Measured

Lighthouse 12, 15 Nov 2026: mobile 98 performance, 100 accessibility, 100 best practices, 100 SEO.
Desktop 100 across the board. No horizontal scroll at 375 px.
