# Deploy

- Domain: **kembar.web.id**, PT JC Indonesia (ResellerCamp), expires 2027-11-15.
- Host: a Cloudflare **Worker** named `kembar`, connected to `Bryyzxm/kembar-site`, serving `site/`
  as static assets. `wrangler.toml` at the repo root is what tells the build what to deploy:
  `name = "kembar"` and `[assets] directory = "./site"`. Without it the Workers Build fails.
- Production URL: `kembar.bryyzxm.workers.dev`. Verified 2026-11-15: pages 200, assets 200 with
  `immutable` caching from `_headers`, security headers present, 404 correct, robots and sitemap 200.

## 1. Nameservers: the only thing left

The domain has no nameservers, so Cloudflare cannot serve it yet. Adding a custom domain to a Worker
requires the zone to be active in the same account.

1. Cloudflare dashboard, Add a site, `kembar.web.id`, Free plan.
2. Copy both nameservers it gives you, exactly.
3. At ResellerCamp, the domain, Nameservers, paste both, save.
4. Wait for the "zone is active" email. Minutes to a few hours.

## 2. Attach the domain

On the Worker, the Domains tab, **Add Domain**, then `kembar.web.id`. Add `www.kembar.web.id` the
same way. Cloudflare writes the DNS record and issues the certificate itself, because the zone lives
in this account. No CNAME to create by hand.

## 3. Redirect www to the apex

A Redirect Rule: when the host is `www.kembar.web.id`, redirect 301 to `https://kembar.web.id`
keeping the path and query. Without it both hosts serve the same page and search engines treat them
as two.

## 4. Prove the waitlist

Submit your own address on the live domain and confirm the Buttondown email arrives. Until that
happens the form is wired but unproven.

## Notes

- The form posts to `buttondown.com`. Never `buttondown.email`: Indonesian ISP DNS resolves that
  domain to the Kominfo block page, so the form would fail silently for local visitors.
- `is-a.dev` was ruled out. Their pull request template requires a non-commercial site.
- Static assets read `_headers` from `site/`, and will read `_redirects` the same way if the site
  ever needs one.
- Canonical, `hreflang`, `og:url`, `sitemap.xml` and `robots.txt` use `https://kembar.web.id`.
