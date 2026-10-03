---
layout: default
title: "Case study: Hireonai — building an AI job portal as founder"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Hireonai: founding and leading an AI job portal</h1>
<p class="post-meta">Startup · Founder & Product Lead · Jan 2026 – Present · hireonai.web.id · github.com/hireonai</p>
<!-- AUDIT: verified = founder/5-engineer team, feature list from resume. Inferred (verify/replace): 'believed keyword search insufficient' motivation framing, MVP/deployment status wording. -->

## The problem

Job portals treat matching as keyword search: your CV is a bag of words, and the platform optimizes for volume, not fit. Career-matching signals that actually matter — semantic overlap between a CV's experience and a JD's responsibilities, skill adjacency, company context — never enter the loop. We believed an LLM-native portal could give candidates genuinely better targeting: CV optimization agents, AI cover letters, and recommendations based on meaning rather than keywords.

## My role & what was built

As **Founder & Product Lead**, I owned the product lifecycle end-to-end — vision, MVP scoping, what NOT to build — and staffed + led the engineering team of **5** (3 fullstack, 2 ML).

- **CV–JD semantic matching**: LLM embeddings score compatibility between a CV and a job description, going past keyword overlap.
- **CV optimization agent**: an LLM agent critiques and rewrites CV bullets against a target JD, and recommends EdX courses to close skill gaps via API.
- **Cover letter generator**: contextual AI drafting in the candidate's voice.
- **Hybrid recommendation engine**: **ChromaDB** vector store + LLM embedding retrieval, similarity scoring and ranking — hybridized with structured filters so results aren't pure semantic soup.
- **Classic ML under the hood**: a transformer-based salary range predictor and a job category classifier (Tech/Finance/HR/Other).

<div class="diagram">
<svg viewBox="0 0 780 150" width="780" role="img" aria-label="Architecture: users interact with the app frontend; services handle CV parsing, embedding scoring in ChromaDB, LLM agents for optimization and cover letters, and classic ML models for salary and category; deployed on GCP via Cloud Run with CI/CD">
  <g fill="none" stroke="currentColor" font-size="12">
    <rect x="10" y="55" width="120" height="44" rx="8" stroke="gray" opacity=".6"/><text x="70" y="74" text-anchor="middle" fill="currentColor" stroke="none">web app</text><text x="70" y="90" text-anchor="middle" fill="currentColor" stroke="none" font-size="10">(candidates)</text>
    <rect x="170" y="15" width="150" height="40" rx="8" stroke="gray" opacity=".6"/><text x="245" y="39" text-anchor="middle" fill="currentColor" stroke="none">CV–JD embedding match</text>
    <rect x="170" y="95" width="150" height="40" rx="8" stroke="gray" opacity=".6"/><text x="245" y="119" text-anchor="middle" fill="currentColor" stroke="none">LLM agent suite</text>
    <rect x="360" y="15" width="130" height="40" rx="8" stroke="gray" opacity=".6"/><text x="425" y="39" text-anchor="middle" fill="currentColor" stroke="none">ChromaDB</text>
    <rect x="360" y="95" width="130" height="40" rx="8" stroke="gray" opacity=".6"/><text x="425" y="119" text-anchor="middle" fill="currentColor" stroke="none">salary / category ML</text>
    <rect x="530" y="55" width="110" height="44" rx="8" stroke="gray" opacity=".6"/><text x="585" y="74" text-anchor="middle" fill="currentColor" stroke="none">GCP services</text><text x="585" y="90" text-anchor="middle" fill="currentColor" stroke="none" font-size="10">Cloud Run · GCE · GCS</text>
    <rect x="670" y="55" width="100" height="44" rx="8" stroke="gray" opacity=".6"/><text x="720" y="81" text-anchor="middle" fill="currentColor" stroke="none">CI/CD</text>
    <line x1="130" y1="65" x2="170" y2="45" stroke="gray"/>
    <line x1="130" y1="89" x2="170" y2="109" stroke="gray"/>
    <line x1="320" y1="35" x2="360" y2="35" stroke="gray"/>
    <line x1="320" y1="115" x2="360" y2="115" stroke="gray"/>
    <line x1="490" y1="35" x2="530" y2="65" stroke="gray"/>
    <line x1="490" y1="115" x2="530" y2="89" stroke="gray"/>
    <line x1="640" y1="77" x2="670" y2="77" stroke="gray"/>
  </g>
</svg>
</div>

## Results

- Team of 5 aligned and shipping toward a deployed MVP (Docker + GitHub Actions → **Cloud Run**), with the matching and recommendation pipeline functional end-to-end.
- Product decisions made and documented: hybrid retrieval over pure semantic, separate agent vs. model tracks, EdX integration as the upskilling loop.

<div class="case-metrics">
  <li><span class="num">5 engineers</span><span class="lbl">cross-functional team led from ideation to deployment</span></li>
  <li><span class="num">4 AI products</span><span class="lbl">matching · CV agent · cover letters · recommendations</span></li>
</div>

## Stack

ChromaDB · LLM embeddings · Google Vertex AI · Cloud Run · Compute Engine · GCS · Docker · GitHub Actions

## Lessons

- Leading engineers means specifying *outcomes and constraints*, not tasks — the hybrid retrieval decision only stuck because the team saw the failure mode in a demo, not because I ordered it.
- Scoping ruthlessly matters more at 5-person scale: every feature we cut was a week of someone's runway we kept.
- LLM-native products live or die on evaluation — we spent more time building quick eval sets than on extra features, and it was the right call.

</div>
