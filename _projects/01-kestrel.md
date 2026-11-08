---
title: Kestrel Flight Computer
role: Designer, Personal Project
dates: October 2026 – Present
skills: KiCad, PCB design, embedded C++, RF
summary: Flight computer for my 4" Wildman Punisher 4, which I'm flying for my NAR Level 2 certification in January 2027.
thumbnail: /assets/img/kestrel/thumb.jpg
permalink: /projects/kestrel/
images:
- src: /assets/img/kestrel/kestrel_block.png
  alt: 'Kestrel block diagram: sensors, flash, GPS, LoRa radio, and four pyro channels around an RP2350B, powered from a 9 V battery through a 3.3 V buck regulator'
  caption: Kestrel block diagram
what:
- Flight computer for my 4" Wildman Punisher 4, which I'm flying for my NAR Level 2 certification in January 2027
- It logs data and sends live telemetry, and will eventually handle dual-deployment recovery, including a later L2200G flight that simulates to about 14,800 ft and Mach 1.7
how:
- Designed the schematic and 4-layer board in **KiCad** (100 × 40 mm, 145 parts)
- RP2350B microcontroller, IMU, high-g accelerometer, two barometers, magnetometer, u-blox GPS, 915 MHz LoRa radio, and flash memory
- Four pyro channels switched on both the high and low side, behind a physical arming switch
- 9 V input with reverse protection and a TPS54202 buck converter for 3.3 V
- Wrote bring-up firmware and a desktop ground station with a live map
results:
- Zero ERC/DRC errors, with every part checked pin by pin against its datasheet and Raspberry Pi's reference design
- Fixed everything an outside schematic review flagged
- PCBWay is building the boards through their Future Innovators sponsorship
- My commercial altimeters keep handling recovery until Kestrel passes ground and flight tests
---

## Design and verification

I switched each e-match on both its high side and its low side, behind a physical arming switch on the airframe, so a charge can only fire when that switch is closed and the processor turns on both transistors. Pull-down resistors keep every gate off while the processor boots, and a small sense current through each e-match shows continuity without firing it.

{% include figure.html src="/assets/img/kestrel/kestrel_pyro.png" alt="One pyro channel: 9 V supply, arming switch, high-side MOSFET, e-match, low-side MOSFET, ground" caption="One of the four pyro channels" %}

I can only afford one board revision, so before ordering I checked each subsystem against a datasheet or reference design and planned a test to prove it once the boards show up.

| Subsystem | Checked against | Proven at bring-up by |
|---|---|---|
| Power | TI's TPS54202 3.3 V reference values; USB-only start-up margin | 3.25–3.35 V at the test point |
| Processor | All 80 RP2350B pins against the pin table and SparkFun's production board | Enumerates over USB |
| Sensors and GPS | Each pinout and SPI mode against its datasheet; u-blox integration manual | Chip ID self-test; 3-D GPS fix |
| Radio | Pinout; link budget of about 29 dB margin at 10 km | Ground-station range test |
| Pyro | MOSFET ratings, gate drive, boot pull-downs | Dummy-load tests, armed and disarmed |
| Layout | Zero ERC/DRC errors; outside review; PCBWay engineering review | Visual inspection of both assembled boards |

## Test plan

On the first flight Kestrel only logs and transmits. A Featherweight Blue Jay and an EasyMini handle recovery. Before I let it control a parachute, its would-fire times from flight 1 have to line up with when the commercial altimeters actually fired. It also has to fire correctly on replayed L2200G simulations without ever firing through the Mach transition. Then it goes through vacuum chamber, inert load, and ground ejection tests.

{% include figure.html src="/assets/img/kestrel/kestrel_test_program.png" alt="Four stages: bench bring-up, flight 1 for the L2 cert with Kestrel logging only, qualifying recovery, then Kestrel in control on the L2200G flight" caption="Test plan before Kestrel controls recovery" %}
