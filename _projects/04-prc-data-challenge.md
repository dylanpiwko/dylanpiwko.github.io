---
title: EUROCONTROL PRC Data Challenge
role: Team Member, Embry-Riddle team "merry-llama"
dates: September – October 2026
skills: Python, LightGBM, CatBoost, SHAP
summary: Predicting aircraft taxi-out time at ten European airports with an Embry-Riddle team.
thumbnail: /assets/img/prc/thumb.jpg
permalink: /projects/prc-data-challenge/
images:
- src: /assets/img/prc/prc_model.png
  alt: Diagram of the team's model with my additions shaded blue
  caption: Team model, my additions in blue
  w: 1.8
- src: /assets/img/prc/prc_versions.png
  alt: Held-out December RMSE falling with each model version
  caption: Held-out error by version (gray points came after the deadline)
  w: 2.0
what:
- Predict aircraft taxi-out time at ten major European airports from about 2 million 2025 departures, scored by RMSE on January and July 2026 flights
- I joined Embry-Riddle's team "merry-llama" with very little Python or machine learning experience and worked on the model for main flights (98.5% of departures)
how:
- Added **CatBoost** models alongside the team's LightGBM models
- Built 16 departure-queue features, like how many planes took off from the same runway in the previous 5 to 20 minutes
- Used **SHAP** on the 1,000 worst predictions, then trained an "airside" taxi-time estimate that doesn't rely on the reported off-block time
- Decided what counted as an improvement before each test, and kept notes on what worked and what didn't across 20+ experiments
results:
- Lowered the team's official RMSE from 276.53 s to 267.34 s
- Taeyun Yoo built the team's best score (265.02 s) and the final pipeline on top of this version, and the final pipeline still uses my CatBoost models and airside estimate
---

## Approach

I started from the team's LightGBM model for main flights and added one thing at a time, testing each change on held-out data. Before each test I decided what result would count as an improvement.

When I looked at the worst predictions with SHAP, most of them were flights whose reported off-block time was more than 10 minutes off. So I trained an airside estimate that doesn't use that time at all.

{% include figure.html src="/assets/img/prc/prc_shap_waffle.png" width="560px" alt="Waffle chart: 82 percent of the 1,000 worst predictions had a reported off-block time more than 10 minutes wrong" caption="Worst 1,000 predictions" %}

## Links

- [Team code on GitHub](https://github.com/taeyunyoo/prc-2026-merry-llama)
