# corm-legal

Public hosting for Corm's legal and support pages. This repo exists so that the URLs Apple's App Store Connect requires on a product page — a reachable **Privacy Policy URL** and **Support URL** — resolve to real pages. Those same pages are linked from the app's paywall and its App Store description.

The authoritative, user-facing versions of Corm's legal documents live inside the Corm iOS app at **Settings → About**. The pages served from this repo render substantively equivalent text.

## Contents

- `index.html` — landing page linking to each document.
- `privacy/index.html` — Corm Privacy Policy, **Version 1.2, Effective September 8, 2026**. Served at `/privacy` (no trailing `.html`).
- `privacy.html` — legacy flat path for the Privacy Policy, kept so older `/privacy.html` links still resolve.
- `terms/index.html` — Corm Terms of Service, **Version 1.2, Effective September 8, 2026**. Served at `/terms`.
- `disclaimer/index.html` — Corm Food Safety & Dietary Disclaimer, **Version 1.1, Effective September 8, 2026**. Served at `/disclaimer`. Hosted because the Terms incorporate it by reference — a document users are bound by must be reachable outside the app.
- `support/index.html` — Support page (contact, common questions). Served at `/support`.
- `CNAME` — GitHub Pages custom domain: `legal.cormtechnologies.com`.
- `.nojekyll` — disable Jekyll processing (we serve raw HTML).
- `.well-known/apple-app-site-association` — Associated Domains / Universal Links manifest. Inert until the app ships an `associated-domains` entitlement (requires a paid Apple Developer team); harmless to host in the meantime.

## Source of truth

The HTML in this repo is rendered from the source documents held in the Corm iOS app repository at `Corm/Resources/*.txt` — the binding copies users accept at the in-app consent gate (Terms of Service and Privacy Policy Version 1.2; Food Safety & Dietary Disclaimer Version 1.1; all Effective September 8, 2026). The root-level `.docx` suite in the app repository is regenerated from the same masters. When a document is revised and counsel re-approves it, regenerate the corresponding HTML here and bump the Effective Date and Version in both places.

## How updates are published

1. Regenerate the affected page(s) from the latest counsel-approved source.
2. Commit and push to `main`. GitHub Pages rebuilds automatically.
3. If the Privacy Policy or Terms changed, bump `ConsentTrackingService.currentPrivacyVersion` (and/or the Terms version) in the Corm iOS app so existing users are re-presented with the consent gate for the new version.

## App Store Connect

The URLs supplied in App Store Connect are:

```
Privacy Policy URL:  https://legal.cormtechnologies.com/privacy
Support URL:         https://legal.cormtechnologies.com/support
```

The Terms of Service is additionally linked from the app's subscription paywall and description (`https://legal.cormtechnologies.com/terms`).

> **Deployment note:** for these URLs to resolve, the `legal` subdomain must be pointed at GitHub Pages at the registrar (Porkbun) and Pages must be enabled for this repo with the custom domain + HTTPS. Until then the subdomain is NXDOMAIN and the App Store Connect URL validation will fail.
