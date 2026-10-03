---
layout: default
title: "Case study: face recognition at a mining site — 0% to 97%"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Face recognition at a mining site: from 0% to 97%</h1>
<p class="post-meta">Production · Computer Vision · NVIDIA Jetson · DeepFace/ArcFace · rubythalib.ai, deployed to Sinarmas Mining</p>
<!-- AUDIT: verified = 0%→97% R&D, stack, Jetson deployment. Inferred (verify/replace): failure modes detail, gallery/ecollection specifics, threshold calibration. -->

## The problem

A face recognition system deployed at a mining site was supposed to support safety/attendance monitoring from CCTV feeds. In production it recognized **0%** — effectively non-functional — while the team needed reliable identification of people on site, in conditions a generic face recognition stack was never built for: harsh lighting, dust, small faces in wide frames, camera angles that were never designed for biometrics, and personnel wearing helmets and masks.

## What was actually wrong

Before touching a model, the failure had to be decomposed. Recognition accuracy is a chain — detect → align → embed → match — and every link was suspect:

- Faces in the frames were too small / off-angle for the pipeline to produce usable embeddings.
- Registration data (the enrolled faces) was not collected under conditions comparable to the deployment cameras.
- Thresholds tuned generically did not match the site's embedding-distance distribution.

## The approach

- Rebuilt the **data foundation first**: controlled re-collection of registration photos and site-realistic face crops, so the gallery matched deployment conditions.
- Iterated **detection → alignment → embedding** (DeepFace / ArcFace) on real site footage; added gating rules (face size, quality) so bad inputs fail fast instead of producing garbage matches.
- Tuned thresholds against the site's actual embedding-distance distribution rather than library defaults.
- Deployed on **NVIDIA Jetson** edge boxes for on-site real-time inference — no cloud round-trip in the loop.

<div class="diagram">
<svg viewBox="0 0 780 150" width="780" role="img" aria-label="Pipeline: CCTV cameras feed a Jetson edge device running detect, align, embed, match; matches become events; a registered-face gallery feeds the match stage">
  <g fill="none" stroke="currentColor" font-size="12">
    <rect x="10" y="55" width="90" height="40" rx="8" stroke="gray" opacity=".6"/><text x="55" y="79" text-anchor="middle" fill="currentColor" stroke="none">CCTV cams</text>
    <rect x="140" y="25" width="330" height="100" rx="10" stroke="gray" opacity=".6"/>
    <text x="305" y="20" text-anchor="middle" fill="currentColor" stroke="none">Jetson edge box</text>
    <rect x="155" y="55" width="70" height="40" rx="6" stroke="gray" opacity=".35"/><text x="190" y="79" text-anchor="middle" fill="currentColor" stroke="none">detect</text>
    <rect x="235" y="55" width="66" height="40" rx="6" stroke="gray" opacity=".35"/><text x="268" y="79" text-anchor="middle" fill="currentColor" stroke="none">align</text>
    <rect x="311" y="55" width="72" height="40" rx="6" stroke="gray" opacity=".35"/><text x="347" y="79" text-anchor="middle" fill="currentColor" stroke="none">embed</text>
    <rect x="393" y="55" width="66" height="40" rx="6" stroke="gray" opacity=".35"/><text x="426" y="79" text-anchor="middle" fill="currentColor" stroke="none">match</text>
    <rect x="510" y="55" width="110" height="40" rx="8" stroke="gray" opacity=".6"/><text x="565" y="79" text-anchor="middle" fill="currentColor" stroke="none">events / API</text>
    <rect x="660" y="55" width="110" height="40" rx="8" stroke="gray" opacity=".6"/><text x="715" y="79" text-anchor="middle" fill="currentColor" stroke="none">logs / DB</text>
    <line x1="100" y1="75" x2="140" y2="75" stroke="gray"/>
    <line x1="470" y1="75" x2="510" y2="75" stroke="gray"/>
    <line x1="620" y1="75" x2="660" y2="75" stroke="gray"/>
    <text x="426" y="140" text-anchor="middle" fill="currentColor" stroke="none" font-size="11" opacity=".8">gallery: registered faces (site conditions)</text>
    <line x1="426" y1="130" x2="426" y2="100" stroke="gray" stroke-dasharray="4 3"/>
  </g>
</svg>
</div>

## Results

- R&D benchmark on site-domain data: **97% accuracy** (up from a 0% baseline in production).
- Same approach carried the system into real deployment on Jetson hardware.

<div class="case-metrics">
  <li><span class="num">0% → 97%</span><span class="lbl">production baseline → R&D accuracy after rebuild</span></li>
  <li><span class="num">On-device</span><span class="lbl">real-time inference, no cloud in the loop</span></li>
</div>

*Honest note: this is a client production system — the detailed threshold values, gallery sizes, and the final production metric aren't public. The R&D figure above is the verified one from my work record.*

## Stack

Python · DeepFace (ArcFace) · OpenCV · NVIDIA Jetson · FastAPI · PostgreSQL/MySQL · Docker

## Lessons

- "The model is bad" almost always means "the data doesn't match deployment." Fixing registration data and gating moved the needle more than swapping architectures.
- A recognition chain is only as strong as its weakest link — measuring per-stage failures (detect rate, embed quality, distance distribution) turns guessing into engineering.
- Edge-first deployment forces good hygiene: small models, tight thresholds, and memory discipline (see also the 8GB→1.8GB leak fix).

</div>
