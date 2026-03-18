# Getting Started

This section walks you through the initial setup of your HALSER board.

## What You Need

- HALSER board
- Power source: NMEA 2000 network or any 5–32 V DC supply
- A waterproof enclosure (see [Enclosures](enclosures.md))
- USB-C cable for programming
- Development environment (see [Software](../software/software.md))

## Quick Start

1. **Wire power and NMEA 2000** — Connect your power source to the 4-pin terminal block. See [Connecting Power and NMEA 2000](connecting-power.md) for wiring details.

2. **Verify power** — The RGB LED should light up when power is applied. The default firmware shows a rainbow animation.

3. **Set up your development environment** — HALSER is a development board. For most use cases, you will need to build and flash custom firmware. See [Software Overview](../software/software.md) for options.

4. **Connect your serial device** — Wire your NMEA 0183, RS-232, or UART device to the appropriate terminal block. See the [Usage](../usage/serial-interfaces.md) section for interface-specific wiring guides.

5. **Flash and test** — Upload your firmware via USB-C and verify that data flows between your serial device and the NMEA 2000 network or WiFi.

!!! tip "Default Firmware"
    HALSER ships with a basic NMEA 0183 → NMEA 2000 gateway firmware for quick evaluation. See [Default Firmware](../software/default-firmware.md) for details. For most practical applications, you will want to develop custom firmware tailored to your specific needs.
