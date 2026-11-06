---
title: Terrier-Sandhawk Two-Stage Rocket
role: Builder and Flyer, Personal Project
dates: January 2025
skills: RockSim, electronic staging, failure analysis
summary: My first two-stage high-power rocket, with electronic staging and a sustainer air-start.
thumbnail: /assets/img/terrier/thumb.jpg
permalink: /projects/terrier-sandhawk/
images:
- src: /assets/img/terrier/rocksim_original.png
  alt: RockSim plot of velocity and altitude against time for the Terrier-Sandhawk
  caption: RockSim simulation
  w: 1.29
- src: /assets/img/terrier/pad_prep.jpg
  alt: Setting the rocket up on pad B1
  caption: Setting up on pad B1
  w: 0.82
- src: /assets/img/terrier/liftoff_crop.jpg
  alt: Liftoff from pad B1
  caption: Liftoff
  w: 0.76
what:
- My first two-stage high-power rocket, a LOC Precision 2.26" Sandhawk sustainer on a Terrier booster (76.9 in, 2,078 g)
- Flew it on a Cesaroni I297 and H180 at Michiana Rocketry on January 31, 2025
how:
- Built the avionics for electronic staging, sustainer air-start, GPS tracking and telemetry. The stages separate 1.0 s after booster burnout and the sustainer lights 0.7 s later
- Simulated the flight in **RockSim** to choose motors and check stability (2.40 static margin)
- Analyzed how the 0.7 s ignition delay, which RockSim doesn't model, changes the trajectory using a 2-D point-mass model
results:
- The delay raised predicted apogee from about 6,590 ft to 6,860 ft
- On the flight the stages didn't separate properly, the sustainer never lit and the upper stage was lost
- Both 9 V batteries were on one sled that most likely slid under boost and disconnected them, which taught me the importance of redundant avionics
---

## Failure analysis

The stages didn't separate properly and the sustainer never lit. Since both happened on the same flight, I looked for something that could cause both.

Every flight computer ran on a 9 V battery, and all of the batteries were mounted to the same sled, which wasn't secured well enough. Under boost acceleration the sled most likely slid down the airframe and disconnected both batteries, so all of the electronics lost power at once.

{% include figure.html src="/assets/img/terrier/terrier_fault_tree.png" width="560px" alt="Fault tree: upper stage lost, from no separation and no sustainer ignition, from both flight computers losing power, from both 9 V batteries disconnecting, from the shared sled sliding under boost" caption="How one loose sled led to both failures" %}

This flight taught me the importance of redundant avionics systems. Having more than one flight computer didn't help, because they all depended on the same mount.

## Staging delay analysis

{% include figure.html src="/assets/img/terrier/rocksim_profile.png" alt="RockSim side view: sustainer and nose cone on the left, booster with orange fins on the right" caption="RockSim model, sustainer on the left (CG 52.5 in, CP 57.9 in from the nose)" %}

RockSim lights the sustainer at the moment the stages separate, so its prediction does not include the 0.7 s wait before sustainer ignition. To model the actual sequence, the upper stage was re-flown from separation with a two-dimensional point-mass model. The sustainer's drag-to-mass ratio was taken from RockSim's coast phase as a function of Mach number, and its ignition mass was fitted to the boost phase using the H180's certified thrust curve. Run with RockSim's own timing, the model matches RockSim's apogee within 3 ft and its peak speed within 0.3%.

{% include figure.html src="/assets/img/terrier/terrier_rocksim_style.png" alt="Velocity and altitude against time with lines for booster burnout, separation, sustainer ignition, sustainer burnout, apogee and ejection" caption="Predicted flight with the 1.0 s separation and 0.7 s ignition delays" %}

With the delay, the sustainer lights at 347 mph instead of 415 mph and peaks at 756 mph instead of 775 mph. Less of the burn happens near Mach 1, where drag is highest, so the predicted apogee rises from about 6,590 ft to 6,860 ft. A 10% change in drag moves this by about 300 ft. Because the sustainer never lit on this flight, the prediction couldn't be checked against flight data.

{% include figure.html src="/assets/img/terrier/terrier_staging_compare.png" width="620px" alt="Velocity from 1 to 6.5 seconds for the RockSim run and for the sequence with the delay" caption="RockSim (gray) vs. delayed ignition (blue)" %}
