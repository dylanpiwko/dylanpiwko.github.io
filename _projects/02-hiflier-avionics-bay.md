---
title: Hi-Flier XL Avionics Bay
role: Avionics Bay Design and PCB Layout, ENGR 100 Team Project
dates: Fall 2026
skills: AutoCAD, KiCad, 3D printing, RockSim, Arduino
summary: 3D-printed avionics bay and sensor board for an Estes Hi-Flier XL, built for ENGR 100 Rocket Science at Michigan.
thumbnail: /assets/img/hiflier/thumb.jpg
permalink: /projects/hiflier-avionics-bay/
images:
- src: /assets/img/hiflier/cad_exploded.png
  alt: Exploded view of the Revision 2 avionics bay. From left, the blue bulkhead with a shock-cord loop, the two purple rails with the green flight computer board between them, the red stop ring, and the orange cap holding a 9 V battery
  caption: Revision 2 of the bay, exploded, with a parts list
  w: 2.18
- src: /assets/img/hiflier/elevator_test.jpg
  alt: The powered sensor board in its printed sled during the elevator test, with its green LED on and the 9 V battery taped above it
  caption: Elevator test
  w: 0.56
what:
- Avionics bay and sensor board for an Estes Hi-Flier XL, built by a five-person team (Team 5, SpaceY) in ENGR 100 Rocket Science at the University of Michigan
- The course project centered on CAD and the payload bay, which had to hold the board and a 9 V battery with no relative motion from launch through landing
- An Arduino Nano Every logs acceleration (ADXL335) and pressure and temperature (BME680) to a microSD card
how:
- Owned the avionics bay. Designed its five parts in **AutoCAD**, printed them in PLA on a Bambu Lab A1, and integrated the board and battery
- Laid out the team's sensor board in **KiCad**
- The board slides into two printed rails glued to a bulkhead, a cap holds the 9 V battery, and a stop ring glued in the tube keeps the sled from moving forward
- Revision 2 adds USB notches so the hot-glued board can be reprogrammed without taking the bay apart
results:
- Passed all six go/no-go tests (bench, two spike tests, pendulum, elevator, and simulation)
- RockSim predicts about 158 ft on the required C11-3 and 464 ft on the D12-5, with stability margins of 3.6 and 3.5 calibers. Both flights are scheduled for November 24, 2026
- Led to [Kestrel](/projects/kestrel/), a personal flight computer for a 4" high-power rocket
---

## Design

The preliminary design review placed the electronics inside a 3D-printed nose cone. The final design keeps a standard nose cone and moves the bay into a BT-60 payload tube, joined to the body tube with an Apogee AC-41.6 coupler. The sled slides in from the aft end, two M3 screws through the tube hold the bulkhead, and the stop ring keeps the sled from moving forward.

{% include figure.html src="/assets/img/hiflier/cad_section.png" alt="Section view of the bay installed in the payload tube. The coupler is on the left, then the bulkhead held by two M3 screws, the flight computer in its rails, the stop ring glued in the tube, and the 9 V battery in the cap cradle, with empty tube toward the nose on the right" caption="The bay installed, with the tube and coupler cut in half. Nose end to the right." %}

| Part | Job | Key detail |
|---|---|---|
| 1. Bulkhead | Closes the aft end, holds the rails, and anchors the shock cord | 39.1 mm diameter, sized for the coupler's 39.37 mm bore |
| 2a, 2c. Rails | Hold the board by its edges | 2c has a cut-out for the slide switch |
| 3. Cap and battery cradle | Joins the front ends of the rails and holds the 9 V battery | 14 mm USB notch, spine 1.4 mm thicker in Revision 2 |
| 4. Stop ring | Glued inside the tube. The cap presses against it so the sled can't move forward | 40.15 mm diameter, cut into a C-ring with a 16 mm USB notch |
| 5. Drill jig | Lines up the holes in the tube | 3.4 mm screw holes, 2.5 mm vents, 5 mm switch hole |

The flight parts weigh about 19 g in PLA. Every part was checked for interference in CAD against the catalog sizes of the tube and coupler before printing.

<div class="shots">
<figure style="flex: 1.9 1 0"><a href="/assets/img/hiflier/autocad_bulkhead_cap.jpg"><img src="/assets/img/hiflier/autocad_bulkhead_cap.jpg" alt="AutoCAD 3D view of the bulkhead, showing the shock-cord loop and the slots that hold the rails" loading="lazy"></a><figcaption>Bulkhead in AutoCAD, with the shock-cord loop and rail slots</figcaption></figure>
<figure style="flex: 2.36 1 0"><a href="/assets/img/hiflier/cad_sled.png"><img src="/assets/img/hiflier/cad_sled.png" alt="Rendering of the assembled sled: 9 V battery in the cap, the stop ring, the board in its rails, and the bulkhead with two M3 screws" loading="lazy"></a><figcaption>Revision 2 sled with the board and battery in place</figcaption></figure>
</div>

### Revision 2

The first printed set was dry-fit with the bare board. Because the board is hot-glued into the sled, Revision 2 is aimed at a bay that ships assembled. It keeps the printed geometry and changes three things:

- The slide switch cut-out moves to the opposite corner of the board, in rail 2c and in the drill jig
- The cap's spine is 1.4 mm thicker
- The cap and stop ring get matching notches, so a USB cable can reach the Arduino from the nose end with the nose cone off

## Build and test

<div class="shots">
<figure style="flex: 0.92 1 0"><a href="/assets/img/hiflier/printing_a1.jpg"><img src="/assets/img/hiflier/printing_a1.jpg" alt="Bambu Lab A1 printer at the U-M 3D Printing Club printing the stop ring, rails, and bulkhead in white PLA" loading="lazy"></a><figcaption>Printing on a Bambu Lab A1</figcaption></figure>
<figure style="flex: 1.22 1 0"><a href="/assets/img/hiflier/printed_parts.jpg"><img src="/assets/img/hiflier/printed_parts.jpg" alt="The printed bulkhead, stop ring, cap, and two rails laid out on a table" loading="lazy"></a><figcaption>The printed parts</figcaption></figure>
<figure style="flex: 1.29 1 0"><a href="/assets/img/hiflier/dry_fit.jpg"><img src="/assets/img/hiflier/dry_fit.jpg" alt="The bare green circuit board seated in the white printed rails between the bulkhead and cap" loading="lazy"></a><figcaption>Dry fit with the bare board</figcaption></figure>
</div>

The parts were printed in PLA at the U-M 3D Printing Club, at 0.20 mm layers with no supports.

{% include figure.html src="/assets/img/hiflier/bambu_studio_slice.jpg" width="760px" alt="Bambu Studio preview of the first plate of bay parts, using 5.88 m and 17.82 g of PLA with a 52 minute print time" caption="The first set of parts sliced in Bambu Studio: 17.82 g of PLA and 52 minutes of printing" %}

The team ran these go/no-go tests before launch:

| Test | Method | Result |
|---|---|---|
| Bench | Board powered on the bench, checking that it logs data and the LEDs work | Pass |
| Spike, accelerometer | Board shaken along each axis | Pass |
| Spike, BME680 | A warm finger on the sensor for temperature, a breath on it for pressure | Pass |
| Pendulum | Board and battery mounted and swung on strings of different lengths | Pass |
| Elevator | Elevator ride with a stop at each level | Pass |
| Simulation | RockSim check of altitude and stability on the required motors | Pass |

<div class="shots">
<figure style="flex: 0.47 1 0"><a href="/assets/img/hiflier/bay_in_tube_2.jpg"><img src="/assets/img/hiflier/bay_in_tube_2.jpg" alt="The finished sled with the board, sensors, and taped battery, and the red coupler fitted over the bulkhead end" loading="lazy"></a><figcaption>Finished sled with the coupler fitted</figcaption></figure>
<figure style="flex: 0.39 1 0"><a href="/assets/img/hiflier/bay_in_tube.jpg"><img src="/assets/img/hiflier/bay_in_tube.jpg" alt="The finished sled with the coupler joined to the white body tube" loading="lazy"></a><figcaption>Coupler joined to the body tube</figcaption></figure>
</div>

## Flight simulation

The course requires a flight on a C11 followed by a flight on a D12. The team's RockSim model includes the bay and its electronics.

{% include figure.html src="/assets/img/hiflier/rocksim_predictions.png" alt="Bar charts comparing the C11-3 and D12-5: apogee 158 ft and 464 ft, max velocity 63 mph and 111 mph, velocity at deployment 11 mph and 26 mph" caption="RockSim predictions for the two required flights" %}

{% include figure.html src="/assets/img/hiflier/rocksim_d12.jpg" alt="RockSim side view of the Hi-Flier XL on a D12-5, 31 in long and 1.64 in in diameter, with the payload mass behind the nose cone" caption="RockSim model on the D12-5: 252.6 g, CG 19.63 in and CP 25.29 in from the nose, a stability margin of 3.45 calibers" %}

## Sensor board

The board runs from a single 9 V battery through 5 V and 3.3 V regulators. The ADXL335 accelerometer feeds the Arduino's analog inputs, and the BME680 and microSD logger connect digitally.

<div class="shots">
<figure style="flex: 2.48 1 0"><a href="/assets/img/hiflier/kicad_3d.jpg"><img src="/assets/img/hiflier/kicad_3d.jpg" alt="KiCad 3D render of the front of the team's sensor board" loading="lazy"></a><figcaption>The sensor board in KiCad's 3D viewer</figcaption></figure>
<figure style="flex: 1.33 1 0"><a href="/assets/img/hiflier/block_diagram_pdr.jpg"><img src="/assets/img/hiflier/block_diagram_pdr.jpg" alt="Block diagram: 9 V battery to a 5 V regulator and 3.3 V regulator, powering the accelerometer, BME680, and SD card reader, all connected to the Arduino Nano Every" loading="lazy"></a><figcaption>Team block diagram from the design review</figcaption></figure>
</div>

## Next: the Smarter Flyer

The next phase of the course is a pitch for the **Smarter Flyer**, a kit built on the Hi-Flier XL for teens and anyone new to rocketry, engineering, or flight computers. It pairs a flight computer that records pressure, temperature, three-axis acceleration, and voltage with a modified rocket and an avionics bay that comes hot-glued and ready to fly. Revision 2 was drawn with that kit in mind, so the board can be reprogrammed without opening the bay.

## Links

- [ENGR 100-980 Rocket Science course site](https://980.engr100.org/)
