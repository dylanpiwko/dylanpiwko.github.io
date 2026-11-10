---
title: EUROCONTROL PRC Data Challenge
role: Team Member, Embry-Riddle team "merry-llama"
dates: September – October 2026
skills: Python, LightGBM, CatBoost, SHAP
summary: Predicting how long departing planes taxi at ten European airports. Most of our worst predictions traced back to bad timestamps in the data.
intro: 'The 2026 PRC Data Challenge asked teams to predict taxi-out time, from when a plane leaves its stand to when it takes off, at ten major European airports, using about 2 million departures from 2025. I joined Embry-Riddle''s team, merry-llama, in September with very little Python or machine learning experience. I was responsible for the model for main flights, which covers 98.5% of departures. My version lowered the team''s official RMSE from 276.53 s to 267.34 s.'
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
---

## Testing one change at a time

I started from the team's LightGBM model and added one change at a time, testing each on held-out December data. Before each run I wrote down what a change had to do to be kept: gain at least 0.5 s and help at 6 or more of the 10 airports. When two options were within 0.3 s, the simpler one won. I also tried hard not to tune to the test month. At one point I turned down a CatBoost weighting that scored 0.5 s better, because I had picked it by looking at December results, the same month I was testing on.

Out of more than 20 experiments, three changes made it into my submitted model. The error-by-version chart at the top shows each step:

- CatBoost models alongside the team's LightGBM models, an idea that came from Dr. Garcia's feedback. December error dropped from 206.9 s to 200.9 s, the biggest single gain.
- 16 departure-queue features, like how many planes took off from the same runway in the previous 5 to 20 minutes. Research on taxi-out time ranks the departure queue among the strongest predictors, and the team's model only had four airport-wide counts. 200.9 s to 198.2 s.
- An airside taxi-time estimate, explained below. 198.2 s to 196.4 s.

## Finding the bad timestamps

Dr. Li suggested looking at the model with SHAP, so I ran it on the 1,000 worst December predictions. Of those, 82% had a reported off-block time that was more than 10 minutes wrong, compared with 6% of all flights. When that timestamp is recorded late, the taxi time looks short, and the model trusts it and predicts too short. Rome alone had 255 of the 1,000.

{% include figure.html src="/assets/img/prc/prc_shap_waffle.png" width="560px" alt="Waffle chart: 82 percent of the 1,000 worst predictions had a reported off-block time more than 10 minutes wrong" caption="Worst 1,000 predictions" %}

So I gave the model a second opinion. I trained an airside estimate that predicts taxi time from airport-side information only, without the reported off-block time, and added it as a feature, so the main model could notice when the two disagree.

## Results

My v5 model is the one that lowered the official RMSE to 267.34 s. Taeyun Yoo then built the team's best leaderboard score, 265.02 s, and the final pipeline on top of it. The final pipeline still uses my CatBoost models and airside estimate.

After the deadline, I tried ADS-B features from OPDI. They lowered held-out error further (the gray points on the chart), but too late to submit.

Our team finished 47th of 94, with an RMSE of 220.23 s. The final ranking was scored on February and June 2026 flights that never appeared on the leaderboard, so that number isn't directly comparable to the January and July scores above. The top three teams scored 176.16, 180.18, and 183.66 s.

## What the top teams did differently

After the challenge, I read the top three teams' write-ups. Most of the gap came from things they did that we didn't:

- They used public ADS-B tracks to see when each plane actually left its stand. That fixes the same off-block time problem my SHAP analysis found, and our final model didn't use ADS-B data at all.
- They modeled which recorded taxi times were really copied schedule times. One team also recovered unmatched flights from their arrival records at the destination.
- They averaged many neural networks or sequence models with their tree models. We only used gradient-boosted trees.

Next time, I'd look for the best raw data source before tuning anything, set aside a test set at the start that I never use for decisions, and try more than one kind of model early.

## Links

- [Final ranking](https://ansperformance.eu/study/data-challenge/dc2026/ranking.html)
- [Team code on GitHub](https://github.com/taeyunyoo/prc-2026-merry-llama)
