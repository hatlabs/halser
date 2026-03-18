# Serial Interfaces Overview

HALSER provides four serial interfaces for connecting different types of devices. This section describes the serial architecture and helps you choose the right interface for your application.

<!-- TODO: Add serial architecture diagram showing all interfaces -->

## Available Interfaces

| Interface | Connector | Signal Level | Typical Use |
|-----------|-----------|-------------|-------------|
| RS-485 RX | 3-pin terminal block | Differential | Receiving NMEA 0183 |
| RS-485 TX | 3-pin terminal block | Differential | Sending NMEA 0183 |
| RS-232 | 3-pin terminal block | ±12 V | Legacy serial devices |
| UART | 3-pin terminal block | 3.3 V / 5 V (jumper) | TTL-level serial |

## Important: Serial Receive Constraint

!!! warning "One Receive Interface at a Time"
    Only **one** serial interface can receive data at a time. The active receive interface is selected in firmware. By default, the RS-485 RX interface is active.

    All interfaces **transmit** the same signal simultaneously — data sent by the firmware appears on all TX interfaces at once.

This design reflects the typical marine use case: a single instrument sends data to HALSER, which converts and forwards it to NMEA 2000 or WiFi.

## Choosing an Interface

| Device Type | Recommended Interface | Notes |
|------------|----------------------|-------|
| NMEA 0183 instruments (wind, GPS, depth, heading) | [RS-485 RX](nmea-0183.md) | Standard for marine instruments |
| AIS transponders | [RS-485 RX](nmea-0183.md) | RS-422 output is electrically compatible with RS-485 |
| Older chart plotters, legacy marine equipment | [RS-232](rs-232.md) | For devices with DB-9 or similar RS-232 ports |
| Victron VE.Direct devices | [UART](uart.md) | Raw UART at 19200 baud |
| GPS modules (bare boards) | [UART](uart.md) | Most GPS modules output TTL UART |
| General-purpose microcontrollers | [UART](uart.md) | Direct MCU-to-MCU communication |

## Interface Details

See the individual pages for wiring instructions and device-specific guidance:

- [NMEA 0183 (RS-485)](nmea-0183.md)
- [RS-232 Devices](rs-232.md)
- [UART Devices](uart.md)
