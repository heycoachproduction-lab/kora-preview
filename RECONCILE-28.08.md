# RECONCILE — 28.08.2026

## Verdict
**`concept2/` is the source of truth.** The live `index.html` in this repo is a plain build of
`02-SITE/concept2/` (`build.py`) with three post-build tweaks. No copy divergence in either direction.

## Repo contents
Built artefact only — no sources:
`README.md · index.html (1 932 659 B) · hero.mp4 (600 372 B) · og.png · robots.txt` (robots = `Disallow: /`).

Last 5 commits:
```
4f24c6f 2026-08-27 20:18:48  KORA introduces herself in the hero and speaks for herself in the Talk section
b8601ec 2026-08-27 20:08:36  Hero copy moves to the edge, off the Core; film starts even if autoplay is blocked
0035f85 2026-08-27 19:25:14  Before you pay, and a conversation that actually goes somewhere
acb9297 2026-08-27 17:58:04  KORA sits beside the conversation
1faa2e4 2026-08-27 16:16:36  Better film, fewer screens
```
Last commit 27.08 20:18:48 = mtime of `concept2/s8-talk.html` (27.08 20:18). Same state.

## Structural comparison
| | live index.html | `python3 build.py` → `concept2/KORA-SITE-CONCEPT-v3.html` |
|---|---|---|
| bytes | 1 932 250 | 2 732 616 |
| `<section id>` count | 17 | 17 |
| section ids | identical order | identical order |
| `<h1>/<h2>` | 17, identical text | 17, identical text |

Section ids (both): `mission · works · problem · solution · why · difference · continuity · telegram ·
steps · always-on · packages · compare · order · asset · talk · faq · contact`.

With every `data:…;base64,…` payload normalised to a token, the two files differ in **exactly 3 lines**:

1. live adds `<meta property="og:url" content="https://heycoachproduction-lab.github.io/kora-preview/">`
2. `og:image` — live absolute URL vs build's relative `og.png`
3. hero video — live `src="hero.mp4"` (external file) vs build's inlined `data:video/mp4;base64,…`

Byte delta 800 366 ≈ base64 of `hero.mp4` (600 372 × 4/3 = 800 496). That is the whole size difference.

## Other local files
`02-SITE/KORA-МАКЕТ-САЙТА-v3-23.08.2026.html` is **byte-identical** (md5 `ff011218…`) to
`concept2/KORA-SITE-CONCEPT-v3.html`; likewise `KORA-МАКЕТ-v3-ШРИФТ-GEIST.html` ↔
`concept2/KORA-SITE-CONCEPT-v3-GEIST.html` (md5 `c961d037…`). They are manual copies of the build output;
`build.py` does not write to them, so they are left untouched by Phase 0 and are now one generation behind.

`concept2/s1-hero.html` is **not** in `build.py`'s parts list (superseded by `s1b-hero-video.html`) —
not edited.

## Consequence
RULE satisfied: fixes applied to `concept2/` sources + rebuild, then the build copied here with the same
three post-build tweaks re-applied (og:url, absolute og:image, external hero.mp4).
