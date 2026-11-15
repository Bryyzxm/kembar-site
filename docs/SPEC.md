---
id: SPEC-landing-page-waitlist
companions: []
sources:
  - README.md
  - _bmad-output/planning-artifacts/research/market-ai-video-editors-that-match-your-editing-2026-11-11/research.md
---

> **Canonical contract.** This SPEC and the files in `companions:` are the complete, preservation-validated contract for what to build, test, and validate. Source documents listed in frontmatter are for traceability. Consult them only if you need narrative rationale or prose color this contract intentionally omits.

# kembar early-access landing page

## Why

**A product page for a product that now exists as one.** kembar started as a folder a few people could install. The page has to sell the hosted editor to solo talking-head creators instead: one long take in, the retakes gone, one word per caption, and the real page on screen at the word that names it. The market research of 2026-11-11 found that style learning is already table stakes and that the verified gap is the bundle, the fidelity and the control. So the page leads with those, and it collects early-access addresses for a hosted product that is still opening in small groups.

## Capabilities

- **CAP-1**
  - **intent:** A first-time visitor can say what kembar does after a ten-second look, in their own language.
  - **success:** Five people from outside the repo, shown the page in either locale for ten seconds, describe it correctly and unprompted.
- **CAP-2**
  - **intent:** A visitor sees real output before reading any claim.
  - **success:** A real frame sits in the hero, and the same take before and after the edit sits above the fold on desktop and at 375px wide.
- **CAP-3**
  - **intent:** A visitor can join the early-access list with an email and knows immediately that it worked.
  - **success:** A submitted address appears in the list within a minute; a malformed address is rejected inline without a page reload.
- **CAP-4**
  - **intent:** A visitor understands what one finished edit contains without leaving the page.
  - **success:** Three cards, each backed by one real frame from the same edit: the captured page, the card, and the counter.
- **CAP-5**
  - **intent:** A visitor understands the product's status and what early access buys them.
  - **success:** The page says the editor is opening in small groups, shows no price and no checkout, and promises no date it cannot keep.
- **CAP-6**
  - **intent:** The page is usable on a phone.
  - **success:** No horizontal scroll at 375px; the join control is reachable within one scroll; Lighthouse mobile performance >= 90.
- **CAP-7**
  - **intent:** The owner can count signups and their source.
  - **success:** Signup count readable in one place; every row carries its UTM or referrer.

## Constraints

- Proof is real frames captured from one edit the editor made (`/Users/bryyzxm/video_edit/edits/video-20261115-110838-2`). No stock footage, no generated screenshots, and no frame the product did not produce.
- Copy describes the abstract properties of a style; it never impersonates a named creator's identity, clips, voice or branding.
- Copy describes a hosted product. It does not mention a local install, a licence, a terminal, a coding agent or a repository.
- No price and no checkout are shown, because neither is settled. The page must not imply a paid plan that does not exist.
- The control section makes four policy statements: no watermark, no duration cap, a switch on every automatic choice, and a failed render costs nothing. Shipping them is a product decision, and any of them must be pulled from the copy if it stops being true.
- Static hosting only, with no server to operate; the form posts to a third-party endpoint and no API key ships in the page.
- Two locales, English and Indonesian, are separate static pages at their own paths, both indexable, chosen from the browser's language with no server, no geo lookup and no redirect loop.

## Non-goals

- Pricing tiers, checkout, or any payment flow.
- Accounts, login, or any part of the app UI.
- A docs site, blog, changelog, or CMS.
- Install instructions, licence terms, or links to the source repository.
- More than two locales, or a language switcher for a third.

## Success signal

Within two weeks of a demo going public, the page turns at least 5% of its visitors into early-access addresses, and every address is attributable to a source without manual cleanup.

## Assumptions

- Audience is solo talking-head creators who already pay for editing, not teams and not established editors.
- Buttondown is the list provider. The form swaps by editing one attribute, so a change costs one line.

## Open Questions

- Does early access charge, and with what packaging? The research points at $19–24 per seat with an upload-minute meter, but the page stays price-silent until the number is settled.
