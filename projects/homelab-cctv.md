---
layout: default
title: "Case study: homelab — real-time CCTV analytics on 4 self-hosted nodes"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Homelab: real-time CCTV analytics on 4 self-hosted nodes</h1>
<p class="post-meta">Self-hosted · Real-time CV · Docker · Tailscale · Frigate · ArcFace · Feb 2025 – Present · this site lives on it</p>
<!-- AUDIT: verified = node list + services (uses page), Frigate person det + ArcFace + WhatsApp alerts (resume). Inferred (verify/replace): detail Distribusi peran STB/power controller — cek uses/index.html. -->

## The problem

Consumer cloud cameras mean monthly fees, cloud-only clips, and zero programmability. I wanted the opposite: a self-owned stack where CCTV analytics run locally, alert me in real time, keep footage private, and double as the infrastructure my other projects run on — including [this website](/blog/moving-this-site-off-github-pages/).

## The architecture

Four nodes, roles split by strengths, all reachable only through a **Tailscale mesh** — nothing public except one Caddy entry point on a small VPS:

- **mini-PC (z6, i3-1215U)** — the always-on node: real-time CCTV analytics (**Frigate**), AI agents, and this website's nginx.
- **workstation (Ryzen 9 9900X + GTX 1660 Super)** — on-demand heavy compute, woken by a power controller when needed.
- **Armbian STB** — network-wide DNS (Pi-hole) + the power controller that wakes the workstation.
- **cloud VPS (sumopod)** — the only public entry: Caddy reverse proxy, TLS, monitoring, LLM routing. Connects home over the mesh; home services never face the internet directly.

<div class="diagram">
<svg viewBox="0 0 780 210" width="780" role="img" aria-label="Diagram: internet reaches Cloudflare, then the VPS running Caddy as the only public entry; a Tailscale mesh connects the VPS to a mini-PC running Frigate CCTV analytics and this website, an STB running DNS and a power controller, and a workstation woken on demand; CCTV cameras feed the mini-PC; Frigate detections trigger WhatsApp alerts and log to a database">
  <g fill="none" stroke="currentColor" font-size="12">
    <rect x="10" y="20" width="90" height="34" rx="8" stroke="gray" opacity=".6"/><text x="55" y="41" text-anchor="middle" fill="currentColor" stroke="none">internet</text>
    <rect x="140" y="14" width="110" height="46" rx="8" stroke="gray" opacity=".6"/><text x="195" y="33" text-anchor="middle" fill="currentColor" stroke="none">Cloudflare</text><text x="195" y="49" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">DNS + edge</text>
    <rect x="290" y="14" width="130" height="46" rx="8" stroke="gray" opacity=".8"/><text x="355" y="33" text-anchor="middle" fill="currentColor" stroke="none">VPS · Caddy</text><text x="355" y="49" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">only public entry</text>
    <rect x="470" y="14" width="300" height="180" rx="12" stroke="gray" stroke-dasharray="6 4" opacity=".7"/>
    <text x="620" y="34" text-anchor="middle" fill="currentColor" stroke="none" font-size="11" opacity=".7">Tailscale mesh (private)</text>
    <rect x="490" y="46" width="130" height="60" rx="8" stroke="gray" opacity=".6"/><text x="555" y="65" text-anchor="middle" fill="currentColor" stroke="none">mini-PC z6</text><text x="555" y="80" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">Frigate · agents</text><text x="555" y="94" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">this website</text>
    <rect x="640" y="46" width="120" height="60" rx="8" stroke="gray" opacity=".6"/><text x="700" y="65" text-anchor="middle" fill="currentColor" stroke="none">Armbian STB</text><text x="700" y="80" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">Pi-hole DNS</text><text x="700" y="94" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">power ctrl</text>
    <rect x="490" y="126" width="270" height="52" rx="8" stroke="gray" opacity=".6"/><text x="625" y="146" text-anchor="middle" fill="currentColor" stroke="none">workstation · Ryzen 9 9900X</text><text x="625" y="161" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">on-demand compute, woken when needed</text>
    <rect x="10" y="120" width="110" height="36" rx="8" stroke="gray" opacity=".6"/><text x="65" y="142" text-anchor="middle" fill="currentColor" stroke="none">CCTV cams</text>
    <path d="M 420 60 L 470 70" stroke="gray"/>
    <line x1="420" y1="45" x2="470" y2="60" stroke="gray"/>
    <path d="M 120 138 c 60 -10 120 -10 180 -10 h 190 v 5" stroke="gray"/>
    <line x1="555" y1="106" x2="555" y2="126" stroke="gray"/>
    <line x1="700" y1="106" x2="700" y2="126" stroke="gray"/>
  </g>
</svg>
</div>

## What the CCTV pipeline does

- **Frigate** ingests camera streams, runs person detection (YOLO), and calls **ArcFace** face recognition on crops of interest.
- Detections log into a database; a notifier container pushes **real-time WhatsApp alerts** with context.
- Everything is Docker Compose, config-as-code; Uptime Kuma watches the services and alerts on failures.

## Results

- A 4-node private cloud that hosts real projects — including this very website, served from the mini-PC through the VPS entry point, [live node stats here](/lab/).
- Real-time alerts on people it recognizes at home, footage and embeddings fully self-owned, zero per-camera fees.

<div class="case-metrics">
  <li><span class="num">4 nodes</span><span class="lbl">mini-PC · STB · workstation · VPS</span></li>
  <li><span class="num">0 exposed</span><span class="lbl">home services; single guarded entry</span></li>
</div>

## Stack

Docker Compose · Tailscale · Frigate · YOLO · ArcFace · Caddy · nginx · PostgreSQL · Uptime Kuma · Pi-hole · WhatsApp API

## Lessons

- "Only public entry point" is the single highest-leverage homelab rule — it makes every other service simpler and safer.
- On-demand compute (wake the workstation only for heavy jobs) gets 90% of the capability at 10% of the power bill.
- Running your own website on your own hardware is the most honest portfolio there is — the infra is the proof.

</div>
