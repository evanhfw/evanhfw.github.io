---
layout: default
title: Evan Hanif Widiatama — AI & Data Engineer
image: /assets/img/og-card.jpg?v=3
permalink: /
---

<div class="hero">
  <h1>Evan Hanif Widiatama</h1>
  <p class="tagline">AI &amp; Data Engineer. I take models from notebook to production — computer vision at mining sites, LLM services, and real-time data pipelines on edge hardware.</p>
  <ul class="hero-stats">
    <li><span class="num">0% → 97%</span><span class="lbl">face recognition, production → R&amp;D accuracy</span></li>
    <li><span class="num">60% → 94%</span><span class="lbl">truck plate OCR accuracy</span></li>
    <li><span class="num">8GB → 1.8GB</span><span class="lbl">edge inference memory, after fixing leaks</span></li>
  </ul>
  <p class="hero-ctas">
    <a href="/projects/face-recognition-mining/">Read the case studies ↓</a>
    <a href="/resume/">Resume</a>
    <a href="https://github.com/evanhfw">GitHub</a>
    <a href="https://www.linkedin.com/in/evanhanif/">LinkedIn</a>
  </p>
</div>

## Case studies

Real systems, real constraints — with architecture diagrams and measured results.

<div class="case-grid">
  <a class="case-card" href="/projects/face-recognition-mining/">
    <p class="kicker">Production · Computer Vision</p>
    <h3>Face recognition at a mining site</h3>
    <p>From 0% accuracy in production to 97% in R&amp;D: data, alignment, thresholds, Jetson deployment.</p>
    <span class="result">0% → 97% · NVIDIA Jetson · DeepFace/ArcFace</span>
  </a>
  <a class="case-card" href="/projects/truck-plate-ocr/">
    <p class="kicker">Production · OCR</p>
    <h3>Truck plate recognition at a disposal site</h3>
    <p>Diagnosed why plate OCR sat at 60% under dust and off-angle cameras, then built a better model.</p>
    <span class="result">60% → 94% accuracy</span>
  </a>
  <a class="case-card" href="/projects/edge-relay-upload/">
    <p class="kicker">Production · Data Engineering</p>
    <h3>Evidence upload pipeline on flaky links</h3>
    <p>Redesigned how Jetson devices ship evidence images over unreliable site networks — from ~40% missing data to zero.</p>
    <span class="result">40% missing → 0% · local relay → GCS</span>
  </a>
  <a class="case-card" href="/projects/hireonai/">
    <p class="kicker">Startup · Founder</p>
    <h3>Hireonai — AI job portal</h3>
    <p>Founded and led a 5-engineer team. LLM CV–JD matching, a ChromaDB recommendation engine, cover letter generation.</p>
    <span class="result">GCP · Vertex AI · ChromaDB</span>
  </a>
  <a class="case-card" href="/projects/homelab-cctv/">
    <p class="kicker">Self-hosted · Real-time</p>
    <h3>Homelab: real-time CCTV analytics</h3>
    <p>Four-node self-hosted infra (Tailscale mesh) running Frigate person detection + ArcFace face recognition with WhatsApp alerts.</p>
    <span class="result">4 nodes · Frigate · live on /lab</span>
  </a>
  <a class="case-card" href="/projects/electricity-forecasting/">
    <p class="kicker">Research · Time Series</p>
    <h3>Electricity load forecasting</h3>
    <p>Feature engineering vs. model complexity for load forecasting: 30-day MAPE of 1–2%, presented at BiCopam 2024.</p>
    <span class="result">MAPE 1–2% · XGBoost · skforecast</span>
  </a>
</div>

## The story in one paragraph

Statistics grad who drifted into computer vision and never left the data side. Now at [rubythalib.ai](https://rubythalib.ai), deployed to Sinarmas Mining / PT Borneo Indobara, building AI systems that run 24/7 on-site: face recognition, plate OCR, and evidence pipelines on NVIDIA Jetson edge devices. Before that: a computer vision internship (YOLOv10→v11, speed estimation), time series research (30-day forecasting at 1–2% MAPE), and a founder stint leading Hireonai's engineering team of 5. On the side I run a four-node homelab that serves this very site — [see it live](/lab/).

## Try the playground

- 🤖 **[Ask AI](/chat/)** — an LLM answers questions about my experience from the data on this site.
- 🖥️ **[/lab](/lab/)** — live CPU/RAM/disk stats from my homelab nodes.
- 💻 **[/terminal](/terminal/)** — a tiny fake shell for people who don't like UIs.
- 🧰 **[/uses](/uses/)** — hardware, software, and services I use daily.

More writing in the [blog](/blog/) — including [how face recognition went from 0% to 97%](/blog/face-recognition-0-to-97/) and [a debugging story about a transparent PNG](/blog/the-transparent-png-that-became-a-black-square/). Certifications live [here](/certifications/).
