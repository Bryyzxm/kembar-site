# Deploy

Target: Cloudflare Pages, connected to this repo, folder `site`.

## Order of operations

1. **Cloudflare Pages project.** Dashboard → Workers & Pages → Create → Pages → Connect to Git →
   pick `Bryyzxm/kembar-site`.
   Build command: none. Output directory: `site`. Root directory: the repo root.
   The first deploy gives you `kembar.pages.dev` (or whatever project name you choose). That URL
   works immediately, with HTTPS, and needs no domain.

2. **Free branded address: `kembar.is-a.dev`.** is-a.dev is a free subdomain service for developers,
   run on GitHub, and it is on the Public Suffix List. That is why it is credible where a "free .com"
   is not.
   - Copy `deploy/is-a-dev.json` into a fork of `is-a-dev/register` as `domains/kembar.json`.
   - Replace `YOUR-GITHUB-USERNAME` and, if your Pages project is not called `kembar`, the CNAME
     target.
   - Open a pull request. Merging takes hours to a day.
   - Adding the domain in Cloudflare **must be done through the API**, not the dashboard: because
     is-a.dev is on the Public Suffix List, the dashboard path fails. Use their helper at
     <https://cf-pages.is-a.dev> or the API endpoint
     `POST accounts/{id}/pages/projects/{project}/domains`.

3. **Canonical and hreflang.** Once the final URL is known, add to both pages:

   ```html
   <link rel="canonical" href="https://URL/">
   <link rel="alternate" hreflang="en" href="https://URL/">
   <link rel="alternate" hreflang="id" href="https://URL/id/">
   ```

   `site/index.html` uses the URL without `/id/`; `site/id/index.html` uses it with `/id/`.

4. **Waitlist.** Replace `YOUR-BUTTONDOWN-USERNAME` in both pages, then submit a real address and
   confirm the confirmation email arrives.

## About email on a free subdomain

Buttondown sends from its own verified domain unless you verify a domain of your own with SPF and
DKIM records. On an is-a.dev subdomain you control only a CNAME, so the confirmation email will come
from Buttondown, not from `kembar.is-a.dev`. That is fine: deliverability is Buttondown's, not the
subdomain's. It only becomes worth changing when you want `hello@yourdomain` to be the sender, which
needs a domain you own.

## Why not a free .com

No registrar gives away `.com`, `.app` or `.co`: the registry charges them roughly $9 to $10 a year
per domain. A site that advertises this is either registering the domain in its own name, funding it
from somewhere else, or not registering it at all. Free *subdomains* of a domain someone else runs
(is-a.dev, eu.org, pages.dev) are a different thing and are safe, because you are not claiming to own
the domain, only a name under it.
