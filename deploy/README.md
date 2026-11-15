# Deploy

Domain: **kembar.web.id**, registered at PT JC Indonesia (ResellerCamp), expires 2027-11-15.
Host: Cloudflare Pages, connected to `Bryyzxm/kembar-site`, folder `site`.

## 1. Put the domain on Cloudflare

1. Cloudflare dashboard, Add a site, `kembar.web.id`, Free plan.
2. Cloudflare shows two nameservers, something like `ada.ns.cloudflare.com` and
   `bob.ns.cloudflare.com`. Copy both exactly.
3. At ResellerCamp: the domain, Nameservers, paste both, save.
4. Wait. Usually minutes, sometimes a few hours. Cloudflare emails you when the zone is active.

Right now the domain has no nameservers at all, so this is the first thing to do.

## 2. Create the Pages project

Workers and Pages, Create, Pages, Connect to Git, pick `Bryyzxm/kembar-site`.

| Field | Value |
|---|---|
| Project name | `kembar-site` |
| Production branch | `main` |
| Build command | empty |
| Root directory | empty |
| Output directory | `site` |

`kembar.pages.dev` is owned by another account, so the project name matters.

## 3. Attach the domain

In the Pages project, Custom domains, add `kembar.web.id`, then add `www.kembar.web.id`. Because the
zone is in the same account, Cloudflare creates the records itself.

Set a redirect rule from `www` to the apex, or the other way round, so both do not serve duplicate
content.

## 4. Check the waitlist end to end

Submit your own address on the live site and confirm the email from Buttondown arrives. Until that
happens the form is wired but unproven.

## Notes

- The form posts to `buttondown.com`. Do not switch it to `buttondown.email`: Indonesian ISP DNS
  resolves that domain to the Kominfo block page, so the form would fail silently for local visitors.
- `is-a.dev` was ruled out. Their pull request template requires the site to be non-commercial, and
  this page is the waitlist for a hosted product.
- Canonical, `hreflang`, `og:url`, `sitemap.xml` and `robots.txt` already use `https://kembar.web.id`.
