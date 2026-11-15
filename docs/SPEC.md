---
id: SPEC-landing-page-waitlist
companions: []
sources:
  - README.md
  - _bmad-output/planning-artifacts/research/market-ai-video-editors-that-match-your-editing-2026-11-11/research.md
---

> **Canonical contract.** This SPEC and the files in `companions:` are the complete, preservation-validated contract for what to build, test, and validate. Source documents listed in frontmatter are for traceability — consult them only if you need narrative rationale or prose color this contract intentionally omits.

# cooked. — landing page with waitlist

## Why

**An opportunity to capture.** cooked. today is a folder with a README: the only people who can find it are the ones already reading GitHub, and the only people who can evaluate it are the ones who already run Claude Code. Meanwhile the market research of 2026-11-11 found that the category's grievance is uniform — tools that force a framing, a caption style and a narrator the user did not ask for, sold on credits that expire when a render fails. cooked. answers that with control, real page captures and logo-per-sentence fidelity, but it has no public surface to say so. A page with a waitlist turns attention from a demo into a list of people who raised their hand for a hosted version that needs no install, before the features are settled.

## Capabilities

- **CAP-1**
  - **intent:** A first-time visitor can say what cooked. does after a ten-second look, in their own language.
  - **success:** Five people from outside the repo, shown the page in either locale for ten seconds, describe it correctly and unprompted.
- **CAP-2**
  - **intent:** A visitor sees real output before reading any claim.
  - **success:** A real before/after frame from the editor sits above the fold on desktop and at 375px wide.
- **CAP-3**
  - **intent:** A visitor can join the waitlist with an email and knows immediately that it worked.
  - **success:** A submitted address appears in the list within a minute; a malformed address is rejected inline without a page reload.
- **CAP-4**
  - **intent:** A visitor learns the three other outputs — shorts from a link, a product video from a URL, a creator teardown — without leaving the page.
  - **success:** Three sections, each backed by one real captured frame, each naming its input type.
- **CAP-5**
  - **intent:** A visitor understands what exists today and what the waitlist buys them.
  - **success:** The page states the editor is free and MIT today, names the hosted early access the waitlist grants, and promises no date it cannot keep.
- **CAP-6**
  - **intent:** The page is usable on a phone.
  - **success:** No horizontal scroll at 375px; the join control is reachable within one scroll; Lighthouse mobile performance ≥ 90.
- **CAP-7**
  - **intent:** The owner can count signups and their source.
  - **success:** Signup count readable in one place; every row carries its UTM or referrer.

## Constraints

- Proof is real frames captured from the editor (`docs/screens/before-talking-head.jpg`, `after-talking-head.jpg`, `after-product-video-1..3.jpg`, `after-teardown.jpg`). No stock footage, no generated screenshots.
- Copy describes the abstract properties of a style; it never impersonates a named creator's identity, clips, voice or branding.
- The editor is free and MIT today. The page must not imply a shipped paid product or a checkout that does not exist.
- Static hosting only — no server to operate; the form posts to a third-party endpoint and no API key ships in the page.
- Two locales, English and Indonesian, are separate static pages at their own paths, both indexable, chosen from the browser's language with no server, no geo lookup and no redirect loop.
- No demo GIF or video exists yet. V1 ships on stills, with a slot the demo drops into without a redesign.

## Non-goals

- Pricing tiers, checkout, or any payment flow.
- Accounts, login, or any part of the app UI.
- A docs site, blog, changelog, or CMS.
- More than two locales, or a language switcher for a third.
- Replacing the README install guide. The page links out; it does not re-explain setup.

## Success signal

Within two weeks of a demo going public, the page turns at least 5% of its visitors into waitlist addresses, and every address is attributable to a source without manual cleanup.

## Assumptions

- Audience is creators and small-business owners who do not yet have a style, not established editors defending one.
- Buttondown is a stand-in provider the form swaps by editing one attribute, since no provider was chosen yet.

## Open Questions

- Does the page show the price band the research found (competitors at $12–41/month), or stay price-silent until launch?
