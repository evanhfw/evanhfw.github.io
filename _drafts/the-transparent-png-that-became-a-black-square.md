---
title: "The transparent PNG that became a black square"
date: 2026-09-27
tags: [images, webp, debugging, caching]
---

*Draft: review lalu publish kalau sudah oke.*

The logo on this site is a circular portrait of me. The original file is a PNG with a transparent background: the photo is a circle, the four corners are transparent, and it sits nicely on any page background.

It weighed 455 KB, which is a lot for a small logo, so I optimized it: resized it and converted it to WebP at quality 88. Result: 20 KB, a 96% saving. Great.

Then a friend looked at the site and asked: "It's supposed to be round, right? Why are the corners black?"

## What happened

When I resized and converted the image, I had flattened it from RGBA (red, green, blue, alpha) to RGB: four channels down to three. The alpha channel is what makes the corners transparent. Without it, the transparent areas became opaque black, and the round portrait turned into a black-cornered square. On a dark background it was easy to miss; on anything lighter it looked broken.

The fix is one detail in the conversion script: keep the image in RGBA when writing the WebP. WebP supports an alpha channel, so nothing is lost:

```python
img = Image.open("logo.png")          # RGBA
img = img.resize((540, 540))          # still RGBA
img.save("logo.webp", "WEBP", quality=88)   # alpha preserved
```

After converting, I checked the mode and the corner pixels programmatically instead of trusting my eyes on a dark editor theme:

```python
print(img.mode)                        # must be RGBA, not RGB
print(img.getchannel("A").getpixel((2, 2)))   # 0 = transparent
```

## The second bug: caches

Fixing the file was not enough. The site is fronted by Cloudflare, and the response header told the story:

```
cf-cache-status: HIT
cache-control: max-age=14400
```

The CDN had cached the broken bytes, and browsers had too, and both would keep serving them for hours. Waiting was not a fix. Instead I bumped the asset URL:

```
/assets/img/logo.webp  ->  /assets/img/logo.webp?v=2
```

A new URL cannot be served from an old cache, so the fixed file reaches everyone immediately. It costs one query string and a note in the template: whenever an asset changes, raise the version.

## Lessons

- Check the mode of an image after every conversion pipeline you write; a silent RGBA to RGB flatten is easy to miss and easy to catch in code.
- Verify images on both a light and a dark background. Dark mode hides black corners.
- A fixed file is not a fixed site until every cache between you and the user agrees. Version asset URLs when it matters.
- And the meta-lesson: look at your own site the way a stranger does, on devices and themes you do not use. The bug was invisible to me for exactly one reason: I was not looking at it fresh.
