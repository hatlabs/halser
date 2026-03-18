# Introduction

HALSER is an ESP32-C3 based development board designed for marine serial interface applications. It bridges legacy serial devices — NMEA 0183 instruments, RS-232 equipment, and UART peripherals — to NMEA 2000 networks and WiFi.

![HALSER board v1.0.1](halser_top_render.jpg)

!!! note "Shop Link"
    Purchase HALSER from the [Hat Labs web shop](https://shop.hatlabs.fi/products/halser).

## Key Features

- **ESP32-C3 microcontroller** — 32-bit RISC-V core, 4 MB flash, WiFi
- **Wide-range power input** — 5–32 V with surge and reverse polarity protection
- **NMEA 2000** — CAN bus interface via 4-pin pluggable terminal block
- **RS-485 TX and RX** — Bidirectional NMEA 0183 communication
- **RS-232** — Legacy serial device support
- **UART** — General-purpose serial (3.3 V / 5 V selectable via jumper)
- **1-Wire and I2C** — Expansion buses for temperature sensors and other peripherals
- **USB-C** — Programming and serial communication
- **RGB status LED** — Visual indication of board state
- **EMC-compliant design** — Won't interfere with navigation or radio equipment
- **Compact form factor** — Fits standard 100×68×50 mm waterproof enclosures

## What's in the Box

<!-- TODO: Verify exact box contents -->

- HALSER board
- 4-pin pluggable screw terminal (NMEA 2000 and power)
- Two 3-pin pluggable screw terminals (serial I/O)
- Two jumper headers (serial configuration)

## Where to Start

- **New to HALSER?** Start with the [Getting Started](getting-started/getting-started.md) guide for hardware setup.
- **Connecting devices?** See the [Usage](usage/serial-interfaces.md) section for wiring and interface details.
- **Building firmware?** The [Software](software/software.md) section covers development options.
- **Looking for specs?** The [Hardware Description](hardware/hardware.md) has detailed technical reference.
