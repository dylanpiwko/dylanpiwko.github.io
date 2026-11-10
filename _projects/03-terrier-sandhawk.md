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
  alt: RockSim plot of velocity and altitude against time for the Terrier-Sandhawk, peaking at about 775 mph and 6,590 ft
  caption: RockSim prediction, about 6,590 ft and 775 mph
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
- Flew on a CTI I297, staging to an H180, at Michiana Rocketry on January 31, 2025
how:
- Built the avionics for electronic staging, sustainer air-start, GPS tracking, and telemetry. The stages separate 1.0 s after booster burnout and the sustainer lights 0.7 s later
- Simulated the flight in **RockSim** to choose motors and check stability (2.40 static margin)
- Chose the staging delays to balance visibility from the ground, altitude, and stability in wind
results:
- With the 0.7 s ignition delay included (RockSim leaves it out), predicted apogee rises from about 6,590 ft to 6,860 ft
- On the flight the stages didn't separate properly, the sustainer never lit, and the upper stage was lost
- Both 9 V batteries were on one sled that most likely slid under boost and disconnected them, which taught me the importance of redundant avionics
---

## Failure analysis

The stages didn't separate properly and the sustainer never lit. Since both happened on the same flight, I looked for something that could cause both.

The sustainer carried only a main parachute, held closed by a Jolly Logic Chute Release in the payload tube. There was no drogue. Below the payload tube, the electronics bay held an Altus Metrum EasyMini for recovery and an EasyTimer for staging, and the EasyTimer's igniter leads ran down the outside of the airframe under aluminum tape to the sustainer motor. Both altimeters ran on 9 V batteries mounted to one balsa sled, inside a coupler held in by two plastic rivets.

My best explanation is that either the balsa sled broke or the rivets sheared. Under boost acceleration the batteries would then slide aft and pull loose from both altimeters, so all of the electronics lost power at once.

{% include figure.html src="/assets/img/terrier/sustainer_cad.png" alt="3-D model of the Terrier-Sandhawk sustainer cut in half lengthwise, showing the nose cone, main parachute with Chute Release, electronics bay, two 9 V batteries on a balsa sled in a coupler held by plastic rivets, igniter leads under aluminum tape, motor mount with the H180, and fins" caption="3-D model of the sustainer as flown, cut in half to show the inside. Positions are approximate." %}

{% include figure.html src="/assets/img/terrier/battery_failure_cad.png" alt="Two close-ups of the electronics bay and battery coupler. As built, both 9 V batteries are connected to the altimeters. In the failure view, the rivets have sheared, the coupler, sled, and batteries have slid aft, and the battery snaps are left behind, so the EasyMini and EasyTimer lose power" caption="The electronics bay and battery coupler as built (top) and the most likely failure during boost (bottom)" %}

{% include figure.html src="/assets/img/terrier/terrier_fault_tree.png" width="560px" alt="Fault tree: upper stage lost, from no separation and no sustainer ignition, from both flight computers losing power, from both 9 V batteries disconnecting, from the shared sled sliding under boost" caption="How one battery mount led to both failures" %}

This flight taught me the importance of redundant avionics systems. Having more than one flight computer didn't help, because they all depended on the same mount.

## Staging delay analysis

The EasyTimer let me set the staging delays myself, so I had to decide what they should be. I wanted a flight that looked good and went high. To me, looking good meant you could clearly see each event from the ground: booster burnout, then separation, then the sustainer lighting. Spacing them farther apart makes each one easier to see, and some delay can add altitude. But the longer the sustainer coasts without thrust, the slower it's going when it lights, and the easier it is for wind to push it off course. I still want to be able to fly in conditions that aren't perfect, so I settled on 1.0 s from booster burnout to separation and another 0.7 s to sustainer ignition.

{% include figure.html src="/assets/img/terrier/rocksim_profile.png" alt="RockSim side view: sustainer and nose cone on the left, booster with orange fins on the right" caption="RockSim model of the full stack, sustainer on the left. The CG (52.5 in from the nose) is 5.4 in ahead of the CP (57.9 in), a static margin of 2.40." %}

RockSim lights the sustainer at the moment the stages separate, so its prediction does not include the 0.7 s wait before sustainer ignition. To model the actual sequence, the upper stage was re-flown from separation with a two-dimensional point-mass model. The sustainer's drag-to-mass ratio was taken from RockSim's coast phase as a function of Mach number, and its ignition mass was fitted to the boost phase using the H180's certified thrust curve. Run with RockSim's own timing, the model matches RockSim's apogee within 3 ft and its peak speed within 0.3%.

{% include figure.html src="/assets/img/terrier/terrier_rocksim_style.png" alt="Velocity and altitude against time with lines for booster burnout, separation, sustainer ignition, sustainer burnout, apogee, and ejection" caption="Predicted flight with both delays. Booster burnout (1.9 s), separation (2.9 s), sustainer ignition (3.6 s), and sustainer burnout (5.2 s) are spaced far enough apart to follow from the ground, and apogee comes at about 6,860 ft." %}

With the delay, the sustainer lights at 347 mph instead of 405 mph and peaks at 756 mph instead of 775 mph. Less of the burn happens near Mach 1, where drag is highest, so the predicted apogee rises from about 6,590 ft to 6,860 ft. A 10% change in drag moves this by about 300 ft. Because the sustainer never lit on this flight, the prediction couldn't be checked against flight data.

{% include figure.html src="/assets/img/terrier/terrier_staging_compare.png" width="620px" alt="Velocity from 1 to 6.5 seconds for the RockSim run and for the sequence with the delay" caption="Velocity from 1 to 6.5 s. RockSim (gray) lights the sustainer at separation, at 405 mph, and peaks at 775 mph. With the 0.7 s delay (blue), the sustainer slows to 347 mph before it lights, then peaks at 756 mph. Lighting slower costs some stability in wind but keeps more of the burn below Mach 1." %}
