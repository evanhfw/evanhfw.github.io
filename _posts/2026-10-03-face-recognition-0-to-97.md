---
title: "Face recognition at a mining site: the road from 0% to 97%"
date: 2026-10-03
tags: [computer-vision, face-recognition, edge, jetson, production]
---

<!-- NOTE(evangelis): semua angka di post ini dari record kerja terverifikasi:
     0% production -> 97% R&D, RAM 8GB->1.8GB & 24GB->8GB, OCR 60%->94%,
     evidence missing ~40%->0%. Mekanisme digeneralisasi (detil klien tidak publik). -->

At a mining site deployment, the face recognition system I inherited recognized exactly **no one**. Not "low accuracy" — 0%. The pipeline ran, cameras streamed, inferences returned — and every identity match was useless. Weeks later, the same system hit **97% accuracy** in R&D validation on site-domain data. This is the middle of that story.

## The setup

The system runs on **NVIDIA Jetson** edge boxes at the site, part of mining safety operations (deployed via [rubythalib.ai](https://rubythalib.ai) to Sinarmas Mining / PT Borneo Indobara). Cameras watch operational areas; the pipeline has to identify personnel in real time, on-device — no cloud loop, because site links can't bet on and latency can't be either.

The stack is a classic recognition chain:

```
camera frame → face detection → alignment → embedding → match against gallery
```

Every stage had to work for the whole thing to work. Production accuracy of 0% meant at least one link was broken — but which?

## What a 0% actually means

A number that low is diagnostic gold: it's too clean for "the model is a bit weak" and too consistent for random failure. Start by decomposing the chain and measuring per-stage behavior. In our case the pattern pointed at the beginning-middle of the pipeline, not the matching logic:

- **Enrollment didn't match deployment.** The gallery of registered faces wasn't collected under conditions comparable to what the site cameras actually see — lighting, distance, angles. Embeddings from clean enrollment photos and embeddings from dusty CCTV crops lived in effectively different neighborhoods.
- **Small, sheared, covered faces.** Detection produced boxes, yes, but many were unusable for reliable embeddings — too small, off-angle, partially covered by helmets and masks. Garbage in, confident garbage out.
- **Generic thresholds.** Match thresholds from library defaults had no relationship to this site's embedding-distance distribution.

## What moved the needle

In rough order of impact:

1. **Fix the data contract before the model.** Registration was redone as a controlled process — capture conditions aligned with deployment reality, quality-gated at enrollment time. The gallery stopped being the weakest link.
2. **Gate the inputs.** Face size and alignment-quality checks before embedding: if a crop isn't good enough to produce a meaningful embedding, it gets rejected *before* it can poison a match. Bad input failing fast beats bad output failing slow.
3. **Tune the matcher to the site, not the library.** Thresholds calibrated against the actual distance distribution of real site embeddings.
4. **Hold the engineering line in production.** The same period included hardening the runtime itself on the Jetsons — cutting RAM usage from **8GB to 1.8GB** (and 24GB to 8GB on the bigger boxes) by hunting down memory leaks, because an OOM-ing edge box is 0% accurate no matter how good the model is.

## Results

- Production baseline: **0%** → R&D validation on site-domain data: **97%**.
- The full stack now runs unattended on-site, edge-first, as part of safety operations.

The honest fine print: this is client production work. The exact final production metrics, gallery size, and threshold values aren't mine to publish. What I can testify to is the verified delta — 0% to 97% — and that the root cause was never "buy a better model."

## Lessons

- **Diagnose before training.** A 0% or a 60% is a map of where the pipeline is broken — measure per stage before you touch a single weight.
- **The data contract beats the model choice.** Most "face recognition doesn't work" war stories are "the gallery and the cameras live in different worlds."
- **Edge forces discipline.** Fixed hardware budgets turn model hygiene and memory hygiene from best practices into survival traits.
- The other war stories from this deployment deserve their own posts: the [trucking plate OCR rescue](/projects/truck-plate-ocr/) (60% → 94%) and the [evidence upload redesign](/projects/edge-relay-upload/) (~40% missing data → 0%).
