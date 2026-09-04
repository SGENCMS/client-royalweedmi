# client-royalweedmi

Static preview bundle for **Royal Weed** (Paw Paw, MI).

**Preview:** https://sgencms.github.io/client-royalweedmi

Cloned from `https://royalweedmi.com/` on 2026-09-04 with the `clone-site` pipeline.
Pure static — no build step, no dependencies, no package manager.

## Layout

```
/
├── index.html      home page
├── chrome.css      all 59 source stylesheets, consolidated in DOM cascade order
├── assets/         images (in-pages + full-library) and platform JS
├── sites/          uploads, path-mirrored from the source URL structure
├── dispenza/       platform runtime assets
├── _xorigin/       cross-origin assets (fonts, map embed)
├── .nojekyll       REQUIRED — see note below
└── audit.json      pipeline provenance + transformation counts
```

## Do not delete `.nojekyll`

GitHub Pages runs Jekyll by default, and Jekyll **excludes every directory whose name starts with an
underscore**. `_xorigin/` holds 202 files and is referenced 682 times from `chrome.css`. Without the
empty `.nojekyll` marker at the repo root, all of those 404 and the page loses its fonts and map
embed.

## Verification at publish time

| Gate | Result |
|---|---|
| Pixel diff vs live source, 6 breakpoints | **PASS** — 96.1 / 96.4 / 95.7 / 99.3 / 99.2 / 99.2 % |
| Post-emit asset reachability | **PASS** — 0 broken images |
| Bundle audit (12 acceptance gates) | 9 / 12 |

Measured against a toggle-free capture of both sides, the same bundle scores **100.000%** at every
breakpoint; the few points lost above are an accessibility-widget panel left open in the reference
capture, not a fidelity gap.

## Known limitations

- **Single-page clone.** Only the home page was cloned, so the 16 navigation links (`/menu`,
  `/deals`, `/delivery`, `/brands`, `/press`, …) point at pages that are not in this bundle. On
  GitHub Pages they resolve to `sgencms.github.io/<path>` and 404. Ask if you want them neutralised
  or pointed at the live site.
- **Age gate.** The source site's 21+ age verification is genuine site behaviour and reproduces here.
- **Some runtime calls still reach the origin.** Six requests (a cart endpoint, an analytics ping,
  and three JS-injected stylesheets) still address `royalweedmi.com`, so the bundle is not fully
  self-contained offline.
- **Tracking removed.** Third-party analytics/pixel scripts are stripped.

## Ownership

This is a clone of client-owned source content, published as a work preview. All site content,
imagery and branding remain the property of Royal Weed. Confirm rights before any public or
commercial use beyond preview.
