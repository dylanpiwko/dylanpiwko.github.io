---
title: Kestrel Flight Computer
role: Designer, Personal Project
dates: October 2026 – Present
skills: KiCad, PCB design, RF
summary: A 4-layer flight computer for my Level 2 rocket. The boards are being built now, and it won't control a parachute until it passes bench and flight tests.
intro: Kestrel is the flight computer I'm designing for my 4" Wildman Punisher 4. It's meant to log flight data, send live GPS and telemetry to the ground, and eventually run dual-deployment recovery on its own. PCBWay is building the first boards now, so none of it has been tested yet. Its first flight, my NAR Level 2 attempt in January 2027, will be logging only.
thumbnail: /assets/img/kestrel/thumb_pcb.jpg
permalink: /projects/kestrel/
images:
- src: /assets/img/kestrel/kestrel_pcb.jpg
  alt: 3-D render of the Kestrel board in KiCad, with the SMA antenna connector on the left, the RP2350B in the middle, and screw terminals for power, arming, and four pyro channels on the right
  caption: Kestrel in KiCad, 100 × 40 mm with 4 layers and 145 parts
---

## What it needs to do

The Level 2 flight, on a K535 to about 7,000 ft, is the easier of the two. The rocket's real target is a later L2200G flight that simulates to about 14,800 ft and Mach 1.7, which I'll only fly once I'm certified and the earlier flights show enough margin. For that flight the board needs dual deployment with backups, GPS tracking I can follow from the ground, and clean data through boost. Commercial boards cover all of that, but usually as two separate products, which is part of why I'm building my own. There's a price comparison at the bottom of this page.

## Design decisions

{% include figure.html src="/assets/img/kestrel/kestrel_block.png" alt="Kestrel block diagram: sensors, flash, GPS, LoRa radio, and four pyro channels around an RP2350B, powered from a 9 V battery through a 3.3 V buck regulator" caption="Block diagram. Everything hangs off one RP2350B microcontroller." %}

Most of the board is a standard sensor package around an RP2350B: an IMU, two barometers, a magnetometer, a u-blox GPS, a 915 MHz LoRa radio, and flash memory for logging. A few parts of it took more thought.

### A separate high-g accelerometer

The L2200G flight should peak around 50 g. Most IMU accelerometers top out well below that, so the data would clip during boost, which is exactly when I want it. I added a separate ±200 g accelerometer to cover that part of the flight.

### Pyro channels that can't fire by accident

The pyro channels are the part of the board that can hurt someone. Each e-match is switched on both its high side and its low side, behind a physical arming switch on the airframe, so a charge can only fire when that switch is closed and the processor turns on both transistors. Pull-down resistors hold every gate off while the processor boots. A small sense current through each e-match shows continuity without firing it.

{% include figure.html src="/assets/img/kestrel/kestrel_pyro.png" alt="One pyro channel: 9 V supply, arming switch, high-side MOSFET, e-match, low-side MOSFET, ground" caption="One of the four pyro channels. Firing takes the arming switch and both transistors." %}

### Power

Everything runs from a 9 V battery through reverse-polarity protection and a TPS54202 buck converter that makes 3.3 V. Once Kestrel starts firing charges, I plan to give the pyro channels their own battery.

## Checking it before ordering

I could only afford one board revision, so before ordering I checked each subsystem against a datasheet or reference design and wrote down the test that would prove it once the boards arrive. The design has zero ERC and DRC errors, and PCBWay's engineers reviewed it before production. PCBWay also sponsored part of the order through their Future Innovators Program.

| Subsystem | Checked against | Proven at bring-up by |
|---|---|---|
| Power | TI's TPS54202 3.3 V reference values; USB-only start-up margin | 3.25–3.35 V at the test point |
| Processor | All 80 RP2350B pins against the pin table and SparkFun's production board | Enumerates over USB |
| Sensors and GPS | Each pinout and SPI mode against its datasheet; u-blox integration manual | Chip ID self-test; 3-D GPS fix |
| Radio | Pinout; link budget of about 29 dB margin at 10 km | Ground-station range test |
| Pyro | MOSFET ratings, gate drive, boot pull-downs | Dummy-load tests, armed and disarmed |
| Layout | Zero ERC/DRC errors; PCBWay engineering review | Visual inspection of both assembled boards |

The right-hand column is a plan. None of those tests have happened yet.

## Before it controls a parachute

On the first flight, Kestrel only logs and transmits while a Featherweight Blue Jay and an Altus Metrum EasyMini handle recovery. Afterward, I'll compare when Kestrel would have fired with when the commercial altimeters actually did. It also has to call the right deployment times on replayed L2200G simulations without ever firing through the Mach transition, where pressure readings jump. After that come vacuum chamber, inert load, and ground ejection tests.

{% include figure.html src="/assets/img/kestrel/kestrel_test_program.png" alt="Four stages: bench bring-up, flight 1 for the L2 cert with Kestrel logging only, qualifying recovery, then Kestrel in control on the L2200G flight" caption="The order Kestrel has to earn its way into controlling recovery" %}

## Where it's going

The end goal for this board is the L2200G flight with Kestrel firing all of the recovery charges. After that, I want to bring the cost per board down enough to build them for more than one rocket.

Eventually, I might try to turn Kestrel into a small business. I think there's a gap in the market for flight computers that are affordable but still capable enough for high-performance flights. Right now, a board with GPS tracking and live telemetry starts at $300, and getting four or more pyro channels too means buying the most expensive one or pairing two separate products:

| Product | What it has | Price |
|---|---|---|
| [Altus Metrum TeleMetrum](https://shop.gag.com/product/telemetrum/) | 2 pyro channels, GPS, telemetry | $300 |
| [Altus Metrum TeleMega](https://locprecision.com/collections/altus-metrum/products/altus-metrum-telemega-altimeter-with-gps) | 6 pyro channels, GPS, telemetry | $400 |
| [Featherweight Blue Raven](https://contrailrockets.com/product/featherweight-blue-raven-altimeter) | 4 pyro channels, IMU, no GPS | $194.49 |
| [Featherweight GPS system](https://wildmanrocketry.com/products/featherweight-gps-system) | GPS tracker and ground station, no pyro channels | $420 |

The Altus Metrum boards also need a separate receiver on the ground, and a Blue Raven plus a Featherweight GPS system comes to over $600. Prices are from each retailer's site in November 2026.
