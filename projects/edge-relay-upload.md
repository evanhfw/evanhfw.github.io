---
layout: default
title: "Case study: evidence upload pipeline on flaky site networks — 40% missing to 0"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Evidence upload pipeline: ~40% missing data → 0%</h1>
<p class="post-meta">Production · Data Engineering · NVIDIA Jetson → relay → Google Cloud Storage · rubythalib.ai, deployed to Sinarmas Mining / PT Borneo Indobara</p>
<!-- AUDIT: verified = ~40%→0% missing, relay architecture (Jetson -> LAN relay -> GCS). Inferred (verify/replace): queue/retry/backoff mechanism details, bookkeeping specifics. -->

## The problem

Evidence images (the visual record of hauling/disposal operations) were going missing: roughly **40%** of data never made it to the cloud. Each Jetson device at the site had to push images directly to **Google Cloud Storage** — but site internet links are slow, intermittent, and shared. Every network hiccup meant permanently lost evidence, and nobody could tell which records were complete.

## Root cause

The architecture coupled two very different things: *capture* (local, fast, reliable) and *upload* (remote, slow, flaky). A direct-to-cloud upload from every device meant any outage = data loss, with no retry surface and no local buffer to fall back on.

## The approach

- Inserted a **relay server on the local site network**: Jetson devices now push images over LAN (fast, near-100% delivery), and the relay owns the cloud upload.
- The relay handles **retries, queuing, and backoff** to Google Cloud Storage independently of capture — an outage delays uploads instead of deleting them.
- Added delivery bookkeeping (what's been uploaded per device) so missing data is *detectable*, not silent.

<div class="diagram">
<svg viewBox="0 0 780 170" width="780" role="img" aria-label="Before: each Jetson uploads directly to GCS over a flaky site link, losing data. After: Jetson devices send over local LAN to a relay that queues, retries, and uploads to GCS">
  <g fill="none" stroke="currentColor" font-size="12">
    <text x="10" y="18" fill="currentColor" stroke="none" font-weight="bold">Before: direct upload</text>
    <rect x="10" y="28" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="65" y="49" text-anchor="middle" fill="currentColor" stroke="none">Jetson A</text>
    <rect x="130" y="28" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="185" y="49" text-anchor="middle" fill="currentColor" stroke="none">Jetson B</text>
    <rect x="250" y="28" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="305" y="49" text-anchor="middle" fill="currentColor" stroke="none">Jetson C</text>
    <path d="M 65 62 v 14 h 240 M 185 62 v 24 h 120 M 305 62 v 14" stroke="gray"/>
    <path d="M 125 76 L 233 100" stroke="#c04848" stroke-dasharray="5 3"/>
    <rect x="240" y="100" width="120" height="30" rx="8" stroke="gray" opacity=".6"/><text x="300" y="119" text-anchor="middle" fill="currentColor" stroke="none">internet (flaky)</text>
    <path d="M 360 115 h 40" stroke="gray"/>
    <rect x="400" y="100" width="120" height="30" rx="8" stroke="gray" opacity=".6"/><text x="460" y="119" text-anchor="middle" fill="currentColor" stroke="none">GCS</text>
    <text x="540" y="119" fill="currentColor" stroke="none" font-size="11" opacity=".8">outage = lost forever</text>

    <text x="10" y="152" fill="currentColor" stroke="none" font-weight="bold">After: local relay</text>
    <rect x="10" y="160" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="65" y="181" text-anchor="middle" fill="currentColor" stroke="none">Jetson A</text>
    <rect x="130" y="160" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="185" y="181" text-anchor="middle" fill="currentColor" stroke="none">Jetson B</text>
    <rect x="250" y="160" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="305" y="181" text-anchor="middle" fill="currentColor" stroke="none">Jetson C</text>
    <rect x="420" y="160" width="120" height="34" rx="8" stroke="gray" opacity=".8"/><text x="480" y="181" text-anchor="middle" fill="currentColor" stroke="none">relay (LAN)</text>
    <text x="480" y="214" text-anchor="middle" fill="currentColor" stroke="none" font-size="11" opacity=".8">queue · retry · backoff</text>
    <path d="M 480 194 v 10 M 460 204 h 40" stroke="gray"/>
    <line x1="120" y1="177" x2="420" y2="177" stroke="gray"/>
    <line x1="240" y1="177" x2="420" y2="177" stroke="gray"/>
    <line x1="360" y1="177" x2="420" y2="177" stroke="gray"/>
    <path d="M 520 195 v 8 h 40 v 62" stroke="gray"/>
    <path d="M 540 177 h 30" stroke="none"/>
    <path d="M 540 177 h 20 v 68 h -20" stroke="gray"/>
    <rect x="420" y="245" width="120" height="30" rx="8" stroke="gray" opacity=".6"/><text x="480" y="264" text-anchor="middle" fill="currentColor" stroke="none">GCS</text>
    <text x="560" y="260" fill="currentColor" stroke="none" font-size="11" opacity=".8">outage = delayed, not lost</text>
  </g>
</svg>
</div>

## Results

- Missing evidence dropped from **~40% to 0%** — delivery became a tracked property, not a hope.
- Site operations no longer lose the visual record during internet outages; uploads resume automatically.

<div class="case-metrics">
  <li><span class="num">~40% → 0%</span><span class="lbl">missing evidence images</span></li>
  <li><span class="num">LAN-first</span><span class="lbl">capture decoupled from cloud upload</span></li>
</div>

## Stack

Python · FastAPI · NVIDIA Jetson · local relay server · Google Cloud Storage · Docker

## Lessons

- "We're losing data" is an architecture bug long before it's a data bug — decoupling capture from upload fixed what no amount of retry-on-device would.
- Systems on flaky links need local buffering as a first-class component, not a nice-to-have.
- Instrument delivery (per-device upload ledger) so failure is loud, not silent.

</div>
