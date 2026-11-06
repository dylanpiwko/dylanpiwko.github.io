---
title: Terrier-Sandhawk Two-Stage Rocket
dates: January 2025
role: Builder and Flyer, Personal Project
skills: RockSim · electronic staging · failure analysis
summary: My first two-stage high-power rocket, with electronic staging. The flight failed, and the failure analysis changed how I build avionics.
thumbnail: /assets/img/terrier/thumb.jpg
permalink: /projects/terrier-sandhawk/
---

## Overview

My first two-stage high-power rocket is a LOC Precision 2.26" Sandhawk sustainer on a Terrier booster, flown on a Cesaroni I297 Skidmark in the booster and an H180 Skidmark in the sustainer. It is 76.9 in long and 2,078 g at liftoff. Because composite motors can't reliably light an upper stage on their own, staging is electronic: the stages separate 1.0 s after booster burnout and the sustainer lights 0.7 s later, once the booster has fallen away. I flew it at Michiana Rocketry on January 31, 2025.

## Individual responsibilities

- Built the rocket and its avionics for electronic separation, sustainer air-start, GPS tracking and telemetry
- Simulated the flight in RockSim to pick motors and check stability (2.40 static margin)
- Analyzed how the 0.7 s ignition delay changes the trajectory (see the write-up below)
- Investigated why the flight failed
    - The stages didn't separate properly, the sustainer never lit, and the upper stage was not recovered
    - Every flight computer ran on a 9 V battery mounted to one sled that wasn't secured well enough; the sled most likely slid down the airframe under boost acceleration and disconnected both batteries

**Lesson:** This flight taught me the importance of redundant avionics systems. Both batteries were on the same sled, so one mounting problem took out all of the electronics at once.

{% include gallery.html images="/assets/img/terrier/pad_prep.jpg | /assets/img/terrier/liftoff_crop.jpg | /assets/img/terrier/hero_climb.jpg" alts="Setting the rocket up on pad B1. | Liftoff from pad B1. | Climbing on the booster." height="320px" caption="(L to R): Setting up on pad B1, liftoff on the I297 booster, climbing before staging" %}

{% include figure.html src="/assets/img/terrier/rocksim_profile.png" alt="RockSim side view: sustainer and nose cone on the left, booster with orange fins on the right." caption="RockSim model: sustainer on the left, booster on the right (CG 52.5 in, CP 57.9 in from the nose)" %}

## Sample write-up: effect of the sustainer ignition delay

RockSim lights the sustainer at the moment the stages separate, so its prediction does not include the 0.7 s wait before sustainer ignition. To model the actual sequence, the upper stage was re-flown from separation with a two-dimensional point-mass model. The sustainer's drag-to-mass ratio was taken from RockSim's coast phase as a function of Mach number, and its ignition mass was fitted to the boost phase using the H180's certified thrust curve. Run with RockSim's own timing, the model matches RockSim's apogee within 3 ft and its peak speed within 0.3%.

{% include figure.html src="/assets/img/terrier/terrier_rocksim_style.png" alt="Velocity and altitude against time with lines for booster burnout, separation, sustainer ignition, sustainer burnout, apogee and ejection." caption="**Figure 1.** *Predicted flight with the 1.0 s separation and 0.7 s ignition delays, in RockSim's plot format.*" %}

With the delay, the sustainer lights at 347 mph instead of 415 mph and peaks at 756 mph instead of 775 mph. Less of the burn happens near Mach 1, where drag is highest, so the predicted apogee rises from about 6,590 ft to 6,860 ft. A 10% change in drag moves this by about 300 ft. Because the sustainer never lit on this flight, the prediction couldn't be checked against flight data.

{% include figure.html src="/assets/img/terrier/terrier_staging_compare.png" width="620px" alt="Velocity from 1 to 6.5 seconds for the RockSim run and for the sequence with the delay." caption="**Figure 2.** *Staging close-up: RockSim's run (gray) against the delayed ignition (blue).*" %}
