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
  alt: "Exploded 3-D view of the Revision 2 bay with numbered parts and a parts list: bulkhead (1), rails 2a and 2c around the flight computer board, stop ring (4), and cap (3) holding the 9 V battery"
  caption: Revision 2 of the bay, exploded, with a parts list
  w: 2.18
- src: /assets/img/hiflier/elevator_test.jpg
  alt: The powered sensor board in its printed sled during the elevator test, with its green LED on and the 9 V battery taped above it
  caption: "Elevator test: pressure altitude should step with each floor"
  w: 0.56
what:
- Avionics bay and sensor board for an Estes Hi-Flier XL, built by a five-person team (Team 5, SpaceY) in [ENGR 100 Rocket Science](https://980.engr100.org/) at the University of Michigan
- The course project centered on CAD and the payload bay, which had to hold the board and a 9 V battery with no relative motion from launch through landing
- An Arduino Nano Every logs acceleration (ADXL335) and pressure and temperature (BME680) to a microSD card
how:
- Owned the avionics bay. Designed its five parts in **AutoCAD**, printed them in PLA on a Bambu Lab A1, and integrated the board and battery
- Helped design the team's sensor board, laid it out in **KiCad**, and programmed it in the **Arduino IDE**
- The board slides into two printed rails glued to a bulkhead, a cap holds the 9 V battery, and a stop ring glued in the tube keeps the sled from moving forward
- Revision 2 adds USB notches so the hot-glued board can be reprogrammed without taking the bay apart
results:
- Passed all six go/no-go tests (bench, two spike tests, pendulum, elevator, and simulation)
- RockSim predicts about 158 ft on the required C11-3 and 464 ft on the D12-5, with stability margins of 3.6 and 3.5 calibers. Both flights are scheduled for November 24, 2026
- Led to [Kestrel](/projects/kestrel/), a personal flight computer for a 4" high-power rocket
---

## Design

The preliminary design review placed the electronics inside a 3D-printed nose cone. The final design keeps a standard nose cone and moves the bay into a BT-60 payload tube, joined to the body tube with an Apogee AC-41.6 coupler. The sled slides in from the aft end, two M3 screws through the tube hold the bulkhead, and the stop ring keeps the sled from moving forward.

{% include figure.html src="/assets/img/hiflier/system_cutaway.png" alt="3-D model of the Hi-Flier XL with the bay installed, cut in half lengthwise, nose to the left: nose cone, 9 V battery in the printed cap cradle, flight computer in the printed rails, bulkhead with shock-cord loop, red coupler, body tube, swept fins, and 24 mm motor mount" caption="The Hi-Flier XL with the bay installed, cut in half lengthwise. Airframe dimensions and fin shape come from the team's RockSim model." %}

| Part | Job | Key detail |
|---|---|---|
| 1. Bulkhead | Closes the aft end, holds the rails, and anchors the shock cord | 39.1 mm diameter, sized for the coupler's 39.37 mm bore |
| 2a, 2c. Rails | Hold the board by its edges | 2c has a cut-out for the slide switch |
| 3. Cap and battery cradle | Joins the front ends of the rails and holds the 9 V battery | 14 mm USB notch, spine 1.4 mm thicker in Revision 2 |
| 4. Stop ring | Glued inside the tube. The cap presses against it so the sled can't move forward | 40.15 mm diameter, cut into a C-ring with a 16 mm USB notch |
| 5. Drill jig | Lines up the holes in the tube | 3.4 mm screw holes, 2.5 mm vents, 5 mm switch hole |

The flight parts weigh about 19 g in PLA. Every part was checked for interference in CAD against the catalog sizes of the tube and coupler before printing.

<div class="shots mid">
<figure style="flex: 1.38 1 0"><a href="/assets/img/hiflier/autocad_bulkhead.jpg"><img src="/assets/img/hiflier/autocad_bulkhead.jpg" alt="AutoCAD 3D view of the bulkhead, showing the shock-cord loop, the rail slots, and a screw hole in the side wall" loading="lazy"></a><figcaption>Bulkhead in AutoCAD, with the shock-cord loop and rail slots</figcaption></figure>
<figure style="flex: 0.64 1 0"><a href="/assets/img/hiflier/autocad_cap.jpg"><img src="/assets/img/hiflier/autocad_cap.jpg" alt="AutoCAD 3D view of the cap: a round plate with slots at the bottom and a tall spine with three diamond-shaped windows" loading="lazy"></a><figcaption>Cap and battery cradle in AutoCAD</figcaption></figure>
</div>

## Revision 2

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

| Test | Method | What it checks | Result |
|---|---|---|---|
| Bench | Board powered on the bench | Power, status LEDs, and logging to the microSD card all work before anything moves | Pass |
| Spike, accelerometer | Board shaken along each axis in turn | Each of the three ADXL335 axes responds, on the right channel | Pass |
| Spike, BME680 | A warm finger on the sensor, then a breath on it | Temperature and pressure readings both react to a quick change | Pass |
| Pendulum | Board and battery mounted and swung on strings of different lengths | The logged swing follows the known motion, and the board and battery stay put while moving | Pass |
| Elevator | Elevator ride with a stop at each floor | Pressure, and the altitude worked out from it, step with each floor | Pass |
| Simulation | RockSim model with the bay on the required motors | Altitude and stability margin are acceptable on the C11-3 and D12-5 | Pass |
{: .tests}

<div class="shots narrow">
<figure style="flex: 0.47 1 0"><a href="/assets/img/hiflier/bay_in_tube_2.jpg"><img src="/assets/img/hiflier/bay_in_tube_2.jpg" alt="The finished sled, nose end up: taped 9 V battery at the top, then the cap, board, and sensors, with the red coupler fitted over the bulkhead at the bottom" loading="lazy"></a><figcaption>Finished sled with the coupler fitted, nose end up</figcaption></figure>
<figure style="flex: 0.39 1 0"><a href="/assets/img/hiflier/bay_in_tube.jpg"><img src="/assets/img/hiflier/bay_in_tube.jpg" alt="The finished sled, nose end up, with the coupler at the bottom joined to the white body tube" loading="lazy"></a><figcaption>Coupler joined to the body tube below</figcaption></figure>
</div>

## Flight simulation

The course requires a flight on a C11 followed by a flight on a D12. The team's RockSim model includes the bay and its electronics.

{% include figure.html src="/assets/img/hiflier/rocksim_predictions.png" alt="Bar charts comparing the C11-3 and D12-5: apogee 158 ft and 464 ft, max velocity 63 mph and 111 mph, velocity at deployment 11 mph and 26 mph" caption="RockSim predictions for the two required flights" %}

{% include figure.html src="/assets/img/hiflier/rocksim_d12.jpg" alt="RockSim side view of the Hi-Flier XL on a D12-5, 31 in long and 1.64 in in diameter, with the payload mass behind the nose cone" caption="RockSim model on the D12-5: 252.6 g, CG 19.63 in and CP 25.29 in from the nose, a stability margin of 3.45 calibers" %}

RockSim flags both configurations as overstable. The usual target is 1 to 2 calibers, and a higher margin makes the rocket weathercock, turning more into the wind after it leaves the rod. For low, slow flights like these, 3.45 to 3.64 calibers is acceptable.

## Sensor board

The board runs from a single 9 V battery through 5 V and 3.3 V regulators. The ADXL335 accelerometer feeds the Arduino's analog inputs, and the BME680 and microSD logger connect digitally.

Helping design this board and lay it out in KiCad is what sparked the interest in flight computers that led to [Kestrel](/projects/kestrel/). Along the way, teams peer-reviewed each other's boards, checking another team's design and getting feedback on their own. All of the programming was done in the Arduino IDE, first in the course's earlier labs and then for this board's flight code, which reads each sensor and logs the data to the microSD card.

<div class="shots">
<figure style="flex: 2.48 1 0"><a href="/assets/img/hiflier/kicad_3d.jpg"><img src="/assets/img/hiflier/kicad_3d.jpg" alt="KiCad 3D render of the front of the team's sensor board" loading="lazy"></a><figcaption>The sensor board in KiCad's 3D viewer</figcaption></figure>
<figure style="flex: 1.33 1 0"><a href="/assets/img/hiflier/block_diagram_pdr.jpg"><img src="/assets/img/hiflier/block_diagram_pdr.jpg" alt="Block diagram: 9 V battery to a 5 V regulator and 3.3 V regulator, powering the accelerometer, BME680, and SD card reader, all connected to the Arduino Nano Every" loading="lazy"></a><figcaption>Team block diagram from the design review</figcaption></figure>
</div>

## Next: the Smarter Flyer

The next phase of the course is a pitch for the **Smarter Flyer**, a kit built on the Hi-Flier XL for teens and anyone new to rocketry, engineering, or flight computers. It pairs a flight computer that records pressure, temperature, three-axis acceleration, and voltage with a modified rocket and an avionics bay that comes hot-glued and ready to fly. Revision 2 was drawn with that kit in mind, so the board can be reprogrammed without opening the bay.
