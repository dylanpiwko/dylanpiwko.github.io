---
title: EUROCONTROL PRC Data Challenge
dates: September 2026 – October 2026
role: 'Team Member, Embry-Riddle Aeronautical University team "merry-llama"'
skills: Python · LightGBM · CatBoost · SHAP
summary: 'My work on Embry-Riddle''s team predicting taxi-out times at 10 European airports. Added CatBoost models, departure-queue features, and an airside estimate.'
thumbnail: /assets/img/prc/thumb.jpg
permalink: /projects/prc-data-challenge/
---

## Overview

EUROCONTROL's Performance Review Commission challenged teams to predict aircraft taxi-out time at ten major European airports using about 2 million 2025 departures, scored by RMSE on flights from January and July 2026. I joined an Embry-Riddle team with very little Python or machine learning experience and worked on the model for main flights, which make up 98.5% of departures.

## Individual responsibilities

- Added CatBoost models alongside the team's LightGBM models
- Engineered 16 departure-queue features, such as same-runway takeoffs in the previous 5 to 20 minutes
- Used SHAP to analyze the 1,000 worst predictions
    - Found that 82% had a reported off-block time more than 10 minutes wrong
    - Trained an "airside" taxi-time estimate that does not depend on it
- Lowered the team's official RMSE from 276.53 s to 267.34 s; teammate Taeyun Yoo built the team's best score (265.02 s) and final pipeline on this version

{% include figure.html src="/assets/img/prc/prc_model.png" alt="Diagram of the team's model with my additions shaded." caption="**Figure 1.** *The team's model, with my additions shaded blue.*" %}

{% include figure.html src="/assets/img/prc/prc_versions.png" width="640px" alt="Held-out December RMSE by model version." caption="**Figure 2.** *Held-out error after each of my changes. Gray points came after the deadline and weren't submitted.*" %}

## Links

- [Team repository on GitHub](https://github.com/taeyunyoo/prc-2026-merry-llama)
