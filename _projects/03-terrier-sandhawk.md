---
title: Terrier-Sandhawk Two-Stage Rocket
role: Builder and Flyer, Personal Project
dates: January 2025
skills: RockSim, electronic staging, failure analysis
summary: My first two-stage rocket. The stages didn't separate, the upper stage was lost, and I traced the likely cause to one battery mount.
intro: 'This was my first two-stage high-power rocket: a LOC Precision 2.26" Sandhawk sustainer on a Terrier booster, 76.9 in long and 2,078 g. I flew it at Michiana Rocketry on January 31, 2025, on a CTI I297 staging to an H180. The booster motor lit and the rocket left the pad, but the stages didn''t separate properly, the sustainer never lit, and the upper stage was never recovered. Most of this page is about why.'
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
---

## Design and staging

I simulated the stack in RockSim to pick motors and check stability. It came out with a 2.40 static margin and a predicted apogee of about 6,590 ft, peaking around 775 mph.

{% include figure.html src="/assets/img/terrier/rocksim_profile.png" alt="RockSim side view: sustainer and nose cone on the left, booster with orange fins on the right" caption="RockSim model of the full stack, sustainer on the left. The CG (52.5 in from the nose) is 5.4 in ahead of the CP (57.9 in), a static margin of 2.40." %}

In the sustainer, an Altus Metrum EasyTimer handled staging and an EasyMini handled recovery. The rocket also carried GPS tracking and telemetry. The sustainer had only a main parachute, no drogue, held closed by a Jolly Logic Chute Release until 400 ft. The EasyTimer's igniter leads ran down the outside of the airframe under aluminum tape to the sustainer motor.

The EasyTimer let me set the staging delays myself, so I had to decide what they should be. I wanted a flight that looked good and went high. To me, looking good meant you could clearly see each event from the ground: booster burnout, then separation, then the sustainer lighting. Spacing them farther apart makes each one easier to see, and some delay can add altitude. But the longer the sustainer coasts without thrust, the slower it's going when it lights, and the easier it is for wind to push it off course. I still want to be able to fly in conditions that aren't perfect, so I settled on 1.0 s from booster burnout to separation and another 0.7 s to sustainer ignition.

## Failure analysis

The stages didn't separate properly and the sustainer never lit. Since both happened on the same flight, I looked for one thing that could cause both.

Both altimeters ran on 9 V batteries mounted to a single balsa sled, inside a coupler that was held in by two plastic rivets. My best explanation is that either the sled broke or the rivets sheared. Under boost acceleration the batteries would then slide aft and pull loose from both the EasyMini and the EasyTimer, so all of the electronics lost power at once.

{% include figure.html src="/assets/img/terrier/terrier_fault_tree.png" width="560px" alt="Fault tree: upper stage lost, from no separation and no sustainer ignition, from both flight computers losing power, from both 9 V batteries disconnecting, from the shared sled sliding under boost" caption="How one battery mount led to both failures" %}

I can't confirm this, because the upper stage was never found, but it's the simplest explanation for both failures happening at once. The flight taught me the importance of redundant avionics. I had two flight computers, but they shared one battery mount, so they failed together.

## Checking the staging prediction

RockSim lights the sustainer the moment the stages separate, so its prediction doesn't include the 0.7 s wait before sustainer ignition. To model the actual sequence, the upper stage was re-flown from separation with a two-dimensional point-mass model. The sustainer's drag-to-mass ratio was taken from RockSim's coast phase as a function of Mach number, and its ignition mass was fitted to the boost phase using the H180's certified thrust curve. Run with RockSim's own timing, the model matches RockSim's apogee within 3 ft and its peak speed within 0.3%.

{% include figure.html src="/assets/img/terrier/terrier_rocksim_style.png" alt="Velocity and altitude against time with lines for booster burnout, separation, sustainer ignition, sustainer burnout, apogee, and ejection" caption="Predicted flight with both delays. Booster burnout (1.9 s), separation (2.9 s), sustainer ignition (3.6 s), and sustainer burnout (5.2 s) are spaced far enough apart to follow from the ground, and apogee comes at about 6,860 ft." %}

With the delay, the sustainer lights at 347 mph instead of 405 mph and peaks at 756 mph instead of 775 mph. Less of the burn happens near Mach 1, where drag is highest, so the predicted apogee rises from about 6,590 ft to 6,860 ft. A 10% change in drag moves this by about 300 ft. Because the sustainer never lit, there's no flight data to check this against.

{% include figure.html src="/assets/img/terrier/terrier_staging_compare.png" width="620px" alt="Velocity from 1 to 6.5 seconds for the RockSim run and for the sequence with the delay" caption="Velocity from 1 to 6.5 s. RockSim (gray) lights the sustainer at separation, at 405 mph, and peaks at 775 mph. With the 0.7 s delay (blue), the sustainer slows to 347 mph before it lights, then peaks at 756 mph. Lighting slower costs some stability in wind but keeps more of the burn below Mach 1." %}
