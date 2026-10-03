---
layout: default
title: "Case study: truck plate OCR at a disposal site — 60% to 94%"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Truck plate recognition at a disposal site: 60% → 94%</h1>
<p class="post-meta">Production · OCR · Computer Vision · rubythalib.ai, deployed to Sinarmas Mining / PT Borneo Indobara</p>
<!-- AUDIT: verified = 60%→94%. Inferred (verify/replace): failure buckets detail, 'feedback dataset' naming, validation details. -->

## The problem

An OCR system reading wheel plates of hauling trucks at a disposal site was stuck around **60% accuracy**. Operations relies on these reads to link each truck to its loads/evidence, so a bad read means missing records. Site conditions were hostile: dust, mud on plates, harsh sun and shadows, angles that put plates at oblique views, and mixed plate formats.

## Diagnosis first

Rather than immediately retraining, I profiled where the 40% of failures came from:

- Failure buckets (unreadable vs. misread vs. wrong box): images with plates too small/sheared for the recognizer dominated.
- Off-angle detections produced skewed crops; generic recognizer characters blur under shear.
- Exposure differences between day/portal/dust conditions changed what "readable" meant.

## The approach

- Built a **feedback dataset** from production misses (annotated crops of failed reads) instead of generic plate data.
- Developed/trained a **new recognition model** targeted at the dominant failure buckets, plus detection-side fixes so boxes arrive upright and tight.
- Validated against held-out site data before shipping to the Jetson boxes, with per-site metric tracking in production.

<div class="diagram">
<svg viewBox="0 0 780 130" width="780" role="img" aria-label="Pipeline: camera captures trucks; detection crops plates; a rebuilt recognizer reads them; validation gates the model before deployment; failed reads feed a correction dataset back into training">
  <g fill="none" stroke="currentColor" font-size="12">
    <rect x="10" y="45" width="110" height="40" rx="8" stroke="gray" opacity=".6"/><text x="65" y="69" text-anchor="middle" fill="currentColor" stroke="none">site cameras</text>
    <rect x="160" y="45" width="110" height="40" rx="8" stroke="gray" opacity=".6"/><text x="215" y="69" text-anchor="middle" fill="currentColor" stroke="none">plate detect</text>
    <rect x="310" y="45" width="120" height="40" rx="8" stroke="gray" opacity=".6"/><text x="370" y="69" text-anchor="middle" fill="currentColor" stroke="none">retrained OCR</text>
    <rect x="470" y="45" width="130" height="40" rx="8" stroke="gray" opacity=".6"/><text x="535" y="69" text-anchor="middle" fill="currentColor" stroke="none">records / evidence</text>
    <line x1="120" y1="65" x2="160" y2="65" stroke="gray"/>
    <line x1="270" y1="65" x2="310" y2="65" stroke="gray"/>
    <line x1="430" y1="65" x2="470" y2="65" stroke="gray"/>
    <path d="M 535 85 v 15 h -415 v -15" stroke="gray" stroke-dasharray="4 3"/>
    <text x="245" y="112" text-anchor="middle" fill="currentColor" stroke="none" font-size="11" opacity=".8">failed reads → labeled crops → retrain loop</text>
  </g>
</svg>
</div>

## Results

- Plate recognition accuracy raised from **~60% to 94%** at the disposal site.
- The retrain-on-failures loop is now the standing improvement path for new failure patterns (mud seasons, new plate types).

<div class="case-metrics">
  <li><span class="num">60% → 94%</span><span class="lbl">recognition accuracy at the disposal site</span></li>
  <li><span class="num">Retrain loop</span><span class="lbl">production failures feed the next model</span></li>
</div>

## Stack

Python · YOLO · custom OCR model · OpenCV · NVIDIA Jetson · PostgreSQL/MySQL

## Lessons

- Profiling failure modes beats model-swapping: 40% of failures were concentrated in one identifiable bucket, and fixing that bucket moved the metric 34 points.
- Production bad reads are free labeled data — the retrain loop compounds.
- Diagnosis is a deliverable: "why 60%" is as valuable as "now 94%".

</div>
