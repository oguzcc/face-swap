# GitHub Pages site

Free deep-link landing for face-swap-app referral codes.

Published at: **https://oguzcc.github.io/face-swap-app/**

## What it serves

| URL | What it does |
|---|---|
| `/` | Marketing landing page with store buttons. |
| `/r/<code>` | Referral landing — shows the code prominently + stashes it in `localStorage` + redirects on tap. Implemented via the 404.html SPA-fallback trick (GitHub Pages is static; no dynamic routes). |
| `/.well-known/apple-app-site-association` | iOS Universal Links manifest. Currently a stub — replace `TEAMID` with the Apple Team ID once the app is in App Store Connect. |
| `/.well-known/assetlinks.json` | Android App Links manifest. Currently a stub — replace `REPLACE_WITH_RELEASE_SHA256_FINGERPRINT` with the release keystore fingerprint once the app is signed for Play Store. |

## Enabling Pages (one-time, owner-only)

```text
GitHub repo → Settings → Pages
  Source: Deploy from a branch
  Branch: main / /docs
  Save
```

Wait ~30s; the URL is then live at `https://oguzcc.github.io/face-swap-app/`.

## Once the app is signed

Both manifest files contain placeholders that need real values for
Universal Links / App Links to actually intercept URL clicks:

- **iOS Team ID**: Apple Developer portal → Membership → Team ID (10-char
  string). Replace `TEAMID` in `apple-app-site-association`.
- **Android release fingerprint**: `keytool -list -v -keystore release.jks`
  → SHA256 row. Replace `REPLACE_WITH_RELEASE_SHA256_FINGERPRINT` in
  `assetlinks.json`.

Until then, deep links degrade to the static landing page — the user reads
the 6-char code, taps the store button, and pastes the code in the app's
*Invite friends* sheet manually. Attribution is still trackable via the
`redeemReferralCode` Cloud Function.
