---
title: Kestrel Flight Computer
dates: September 2026 – Present
role: Designer, Personal Project
skills: KiCad · PCB design · embedded C++ · RF
summary: A four-layer rocket flight computer I'm designing for my NAR Level 2 rocket, with GPS, LoRa telemetry and four armed pyro channels.
thumbnail: /assets/img/kestrel/thumb.jpg
permalink: /projects/kestrel/
---

## Overview

Kestrel is a flight computer I'm designing for my 4-inch Wildman Punisher 4, the rocket I'm flying for my NAR Level 2 certification in January 2027. It logs flight data, sends live telemetry and is built to eventually run dual-deployment recovery, including on a later L2200G flight that simulates to about 14,800 ft and Mach 1.7. The four-layer, 100 × 40 mm board has 145 parts and is being made by PCBWay through their Future Innovators sponsorship.

## Individual responsibilities

- Designed the schematic and four-layer PCB in KiCad
    - RP2350B microcontroller with an IMU, high-g accelerometer, two barometers, magnetometer, u-blox GPS, 915 MHz LoRa radio and flash logging
    - Four pyro channels switched on the high and low side behind a physical arming switch
    - 9 V input with reverse protection, regulated to 3.3 V by a TPS54202 buck converter
- Verified the design before ordering, since my budget allows one board revision
    - Checked every part pin by pin against its datasheet and Raspberry Pi's reference design
    - Reached zero KiCad ERC/DRC errors and fixed the items an outside review flagged
- Developed bring-up firmware and a desktop ground station with a live map and pyro continuity
- Planned a staged flight program that keeps commercial altimeters in charge of recovery until Kestrel passes ground and flight tests

{% include figure.html src="/assets/img/kestrel/kestrel_block.png" alt="Kestrel block diagram: sensors and flash on SPI and I2C into an RP2350B; GPS, LoRa radio and four pyro channels behind an arming switch; 9 V battery to a 3.3 V buck regulator." caption="System block diagram. The pyro channels draw power through the arming switch." %}

## Design details

### Pyro channel safety

Each pyro channel switches the e-match on both its high side and its low side, behind a physical arming switch on the airframe. A charge can only fire when the switch is closed and the processor turns on both transistors. Pull-down resistors hold every gate off while the processor boots, and a small sense current through each e-match shows continuity without firing it.

{% include figure.html src="/assets/img/kestrel/kestrel_pyro.png" alt="One pyro channel: 9 V supply, arming switch, high-side MOSFET on GPIO A, e-match, low-side MOSFET on GPIO B, ground." caption="**Figure 1.** *One of four pyro channels. Three independent conditions must all be true to fire.*" %}

### Verification before ordering

Because I can only afford one board revision, I checked each subsystem against a datasheet or reference design before ordering, and planned a specific test to prove it once the boards arrive.

| Subsystem | Checked against | Proven at bring-up by |
|---|---|---|
| Power | TI's TPS54202 3.3 V reference values; USB-only start-up margin | 3.25–3.35 V at the test point |
| Processor | All 80 RP2350B pins against the pin table and SparkFun's production board | Enumerates over USB |
| Sensors and GPS | Each pinout and SPI mode against its datasheet; u-blox integration manual | Chip ID self-test; 3-D GPS fix |
| Radio | Pinout; link budget of about 29 dB margin at 10 km | Ground-station range test |
| Pyro | MOSFET ratings, gate drive, boot pull-downs | Dummy-load tests, armed and disarmed |
| Layout | Zero ERC/DRC errors; outside review; PCBWay engineering review | Visual inspection of both assembled boards |

### Flight plan

On the first flight Kestrel only logs and transmits, while a Featherweight Blue Jay and an EasyMini handle recovery. Before it controls a parachute, its would-fire times from flight 1 have to match the commercial altimeters, it has to fire correctly on replayed simulated L2200G flights and never during the Mach transition, and it has to pass vacuum-chamber, inert-load and ground ejection tests.
