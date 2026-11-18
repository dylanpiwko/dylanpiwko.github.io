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
  caption: Held-out error by version, gray after the deadline
  w: 1.7
what:
- Predict aircraft taxi-out time at ten major European airports from about 2 million 2025 departures, scored by RMSE on January and July 2026 flights
- Joined Embry-Riddle's team "merry-llama" with only two weeks left in the challenge and very little Python or machine learning experience, so the tools had to be learned quickly
how:
- Responsible for the model for main flights, which covers 98.5% of departures
- Added **CatBoost** models alongside the team's LightGBM models
- Built 16 departure-queue features, like how many planes took off from the same runway in the previous 5 to 20 minutes
- Used **SHAP** on the 1,000 worst predictions, then trained an "airside" taxi-time estimate that doesn't rely on the reported off-block time
- Decided what counted as an improvement before each test, and kept notes on what worked and what didn't across 20+ experiments
results:
- Lowered the team's official RMSE from 276.53 s to 267.34 s
- Taeyun Yoo built the team's best score (265.02 s) and the final pipeline on top of this version. The final pipeline still uses these CatBoost models and the airside estimate
---

## Approach

The chance to join came with only two weeks left, so the first job was learning fast. The team's LightGBM model for main flights was taken apart feature by feature until each one made sense, then rebuilt locally until it matched the team's score, before anything was changed.

From there, changes went in one at a time. Each was tested on held-out data against a bar for improvement set before the test, so a lucky result couldn't be mistaken for a real gain. Three changes held up:

- **CatBoost models alongside LightGBM.** The two build their trees differently, so their errors partly cancel when the predictions are averaged.
- **16 departure-queue features** that describe how busy the airport is, like how many planes took off from the same runway in the previous 5 to 20 minutes.
- **An airside taxi-time estimate.** SHAP on the worst predictions showed that most of them were flights whose reported off-block time was more than 10 minutes off, so this estimate was trained without that time at all.

{% include figure.html src="/assets/img/prc/prc_shap_waffle.png" width="560px" alt="Waffle chart: 82 percent of the 1,000 worst predictions had a reported off-block time more than 10 minutes wrong" caption="Worst 1,000 predictions" %}

## Final results

The team finished 47th of 94, with an RMSE of 220.23 s. The final ranking was scored on February and June 2026 flights that never appeared on the leaderboard, so that number isn't directly comparable to the January and July scores above. The top three teams scored 176.16, 180.18, and 183.66 s.

The model splits departures three ways. For the 98.5% of flights with a reported off-block time, takeoff time minus off-block time gives a rough taxi time, and per-airport LightGBM and CatBoost models predict how far off that rough time is, using the team's features, the queue features, and the airside estimate. Their predictions are averaged. Flights without an off-block time use the team's models averaged with the airside estimate (1.4%), or a model based on the type of record at Rome (0.1%). Because the main model starts from the reported off-block time, a wrong off-block time still limits how accurate it can be.

The top three teams' write-ups show where most of the gap came from:

- They used public ADS-B tracks to see when each plane actually left its stand. That fixes the same off-block time problem the SHAP analysis found, and the team's final model didn't use ADS-B data at all.
- They modeled which recorded taxi times were really copied schedule times. One team also recovered unmatched flights from their arrival records at the destination.
- They averaged many neural networks or sequence models with their tree models. The team's model used only gradient-boosted trees.

Lessons for the next data challenge or machine learning project:

- Look for the best raw data source before tuning the model
- Set aside a test set at the start and never use it to make decisions
- Find out early which small group of flights causes most of the error
- Try more than one kind of model from the start

## Links

- [Final ranking](https://ansperformance.eu/study/data-challenge/dc2026/ranking.html)
- [Team code on GitHub](https://github.com/taeyunyoo/prc-2026-merry-llama)
