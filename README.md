# Kamilia legal pages

Static HTML for App Store Connect **Privacy Policy URL** and **Support URL**.

**Method:** same as [PikCal `docs/legal`](https://github.com/raffmag/pikcal/tree/main/docs/legal) — self-contained site, deploy to GitHub Pages, link from the iOS app.

## Pages

| File | ASC / app use |
|------|----------------|
| `index.html` | Landing |
| `privacy.html` | **Privacy Policy URL** |
| `terms.html` | Terms / EULA (paywall later) |
| `support.html` | **Support URL** |
| `styles.css` | Shared Qamra / sakīna styling |
| `logo.png` | Brand mark (from App Icon) |

## Live URLs (after deploy)

Default host matches PikCal’s pattern (`username.github.io/app-legal/`):

```
https://raffmag.github.io/kamilia-legal/
https://raffmag.github.io/kamilia-legal/privacy.html
https://raffmag.github.io/kamilia-legal/terms.html
https://raffmag.github.io/kamilia-legal/support.html
```

These are wired in `Kamilia/App/Config.swift` → `Config.Legal`.

## Deploy (PikCal method)

### Option A — dedicated repo `kamilia-legal` (recommended, same as `pikcal-legal`)

```bash
# one-time
mkdir -p /tmp/kamilia-legal && cd /tmp/kamilia-legal
git init
cp -R /Users/mag/Documents/saas/Kamilia/docs/legal/* .
# remove this README from the public root if you prefer, or keep it
git add .
git commit -m "Kamilia legal site"
gh repo create raffmag/kamilia-legal --public --source=. --push

# GitHub → Settings → Pages → Deploy from branch: main / root
```

After Pages is live, open the privacy URL in Safari (reviewers will).

### Option B — re-sync after content edits

```bash
cd /path/to/kamilia-legal
cp -R /Users/mag/Documents/saas/Kamilia/docs/legal/* .
git add -A && git commit -m "Update legal pages" && git push
```

### Option C — preview locally

```bash
cd /Users/mag/Documents/saas/Kamilia/docs/legal
python3 -m http.server 8765
# open http://127.0.0.1:8765/privacy.html
```

## App wiring

| Surface | Behavior |
|---------|----------|
| ASC Privacy Policy | `Config.Legal.privacyPolicyURL` |
| ASC Support | `Config.Legal.supportURL` |
| In-app You → Privacy / Support | Same URLs + embedded Swift copy for offline reading |
| Email fallback | `support@kamilia.app` |

## Content rules (product + Apple)

- Honest: estimates only; no contraception / “safe days”
- Local-first: no claimed cloud unless implemented
- Contact + delete/export paths must match the shipping app
- Update **Updated** date when material changes

## Checklist before submit

- [ ] Pages deployed and return HTTP 200
- [ ] Privacy + Support URLs set in App Store Connect
- [ ] In-app links open the live pages
- [ ] `support@kamilia.app` inbox monitored (or change email everywhere)
