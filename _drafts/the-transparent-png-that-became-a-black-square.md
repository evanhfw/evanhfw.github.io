---
title: "The transparent PNG that became a black square"
date: 2026-09-27
tags: [debugging, images, webp, caching, pipelines]
---

A tiny bug with a long root cause chain: the site logo — a portrait with a transparent background — started rendering as a **black square** on parts of the site. Wrong armor, wrong weapon, wrong path; every layer of the asset pipeline got to take a turn being guilty.

## The symptom

One file, `circleprofile.webp`, was supposed to be a circular-cropped portrait with alpha transparency. On some surfaces it looked right; as a favicon or when converted through certain paths, the transparent regions turned black. Nothing else on the site was affected. Classic "it depends on who's asking" bug.

## Suspects, in order

1. **The WebP itself** — lossy WebP handles alpha fine, but some toolchains in the chain flatten alpha onto black instead of white.
2. **The PNG source** — transparency semantically lives in PNG; if the master PNG's alpha channel was stripped somewhere upstream, everything downstream inherits the problem.
3. **The conversion script** — `PIL.Image.convert("RGB")` composites nothing: it drops the alpha channel and whatever was "transparent" becomes its raw RGB underpainting — often black.
4. **Caching** — after fixing the file, old bytes still lived in browser and CDN caches; the cache-busting `?v=` query param told the truth only if someone remembered to bump it.

## The actual bug

The generator script did `sq_rgb = sq.convert("RGB")` once and then used that *flattened* version for downstream artifacts. Any consumer that needed transparency was getting an RGB image whose alpha had been silently discarded — the transparent background baked in as black pixels. The fix was structural, not cosmetic:

- Keep the **RGBA master** as the source for anything that must stay transparent (logo WebP, favicons).
- Convert to RGB only for genuinely opaque outputs (apple-touch-icon, the OG card).
- After regenerating, **bump the `?v=` version** on every reference (`_config.yml` logo, head-custom favicons) so caches actually let go of the old black square.

## Why it stuck with me

- **Alpha isn't metadata; it's data.** "Transparent" isn't a property that survives all conversions by default — it dies the moment you collapse to RGB without compositing.
- One upstream flattening poisons every consumer downstream. The bug appeared in surfaces far from the line of code that caused it.
- The last mile of any asset fix is cache invalidation. A correct file with an unchanged version param looks *exactly* like a broken one to a returning visitor.

The full pipeline is open: [gen_assets.py in the deploy repo](https://github.com/evanhfw) — crop → resize → format-specific saves → favicon set → OG card, all from one RGBA master.
