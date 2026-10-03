---
layout: default
title: "Case study: electricity load forecasting — 30-day MAPE of 1–2%"
---

<div class="case">

<p class="back-link"><a href="/projects/">← All case studies</a></p>
<h1>Electricity load forecasting: feature engineering vs. model complexity</h1>
<p class="post-meta">Research · Time Series · XGBoost · skforecast/sktime · sliding-window CV · Universitas Sebelas Maret · BiCopam 2024</p>
<!-- AUDIT: verified = grant research, sliding-window CV, 30-day MAPE 1–2%, BiCopam 2024, thesis topic. Inferred (verify/replace): feature-tool details (lags/rolling/calendar), Shapley usage scope. -->

## The problem

Electricity load forecasting has a hidden trap: short horizons look great in notebooks, but operations need **30-day forecasts** — where naive models fall apart and leakage quietly inflates every metric. As a research assistant on a grant-funded project, the goal was high-accuracy load/regression forecasting that would survive an honest long-horizon validation, and to identify which configuration got there with the lowest error.

## The approach

- Built the pipeline around **sliding-window cross-validation** — the honest way to score long-horizon forecasts, where every fold's test window is strictly in the future relative to its training window.
- Ran **feature engineering** as the primary lever: lag matrices, rolling statistics, calendar/seasonal features — systematically compared against raw-form model capacity.
- Modeled with **XGBoost** inside **skforecast/sktime** frameworks; used **Shapley values** to attribute which features actually carried signal.
- Validated on real sequential consumption data and reported **MAPE across the full 30-day horizon**, not just the easy first days.

<div class="diagram">
<svg viewBox="0 0 780 150" width="780" role="img" aria-label="Pipeline: raw consumption series is cleaned and turned into lag, rolling, and calendar features; sliding-window cross-validation trains XGBoost across folds; Shapley values explain feature importance; final output is a 30-day forecast with honest MAPE">
  <g fill="none" stroke="currentColor" font-size="12">
    <rect x="10" y="55" width="120" height="40" rx="8" stroke="gray" opacity=".6"/><text x="70" y="79" text-anchor="middle" fill="currentColor" stroke="none">load series</text>
    <rect x="170" y="55" width="130" height="40" rx="8" stroke="gray" opacity=".6"/><text x="235" y="72" text-anchor="middle" fill="currentColor" stroke="none">features</text><text x="235" y="87" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">lags · rolling · calendar</text>
    <rect x="340" y="55" width="150" height="40" rx="8" stroke="gray" opacity=".6"/><text x="415" y="72" text-anchor="middle" fill="currentColor" stroke="none">sliding-window CV</text><text x="415" y="87" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">future-only test folds</text>
    <rect x="530" y="55" width="110" height="40" rx="8" stroke="gray" opacity=".6"/><text x="585" y="79" text-anchor="middle" fill="currentColor" stroke="none">XGBoost</text>
    <rect x="680" y="55" width="90" height="40" rx="8" stroke="gray" opacity=".8"/><text x="725" y="72" text-anchor="middle" fill="currentColor" stroke="none">30-day</text><text x="725" y="87" text-anchor="middle" fill="currentColor" stroke="none" font-size="10.5">forecast</text>
    <rect x="530" y="110" width="110" height="34" rx="8" stroke="gray" opacity=".6"/><text x="585" y="131" text-anchor="middle" fill="currentColor" stroke="none" font-size="11">Shapley attribution</text>
    <line x1="130" y1="75" x2="170" y2="75" stroke="gray"/>
    <line x1="300" y1="75" x2="340" y2="75" stroke="gray"/>
    <line x1="490" y1="75" x2="530" y2="75" stroke="gray"/>
    <line x1="640" y1="75" x2="680" y2="75" stroke="gray"/>
    <line x1="585" y1="95" x2="585" y2="110" stroke="gray" stroke-dasharray="4 3"/>
  </g>
</svg>
</div>

## Results

- **30-day horizon MAPE of 1–2%** on real sequential data — sustained across the horizon, not cherry-picked windows.
- A clear, thesis-backed answer: careful **feature engineering** outperformed simply adding model capacity, with the lowest-error configuration identified and documented.
- Methodology + results presented orally at **BiCopam 2024** (Brawijaya International Conference on Pure and Applied Mathematics). Thesis work built directly on this comparison.

<div class="case-metrics">
  <li><span class="num">MAPE 1–2%</span><span class="lbl">30-day horizon, sliding-window CV</span></li>
  <li><span class="num">BiCopam 2024</span><span class="lbl">methodology presented internationally</span></li>
</div>

## Stack

Python · XGBoost · skforecast · sktime · Shapley values · pandas

## Lessons

- Validation design IS the research: sliding-window CV is the difference between a real long-horizon result and a leakage illusion.
- On tabular time series, engineered features beat raw capacity more often than tutorials admit.
- Shapley attribution turns "the model works" into "we know why it works" — which is what made the thesis defensible.

</div>
