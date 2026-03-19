# Serial Interfaces Overview

HALSER provides three physical serial interfaces:

- **RS-485** — Differential signaling, standard for NMEA 0183
- **RS-232** — Legacy serial voltage levels
- **UART** — Raw TTL-level serial (3.3 V or 5 V, selectable via jumper)

Each interface has its own terminal block connector on the board.

<!-- TODO: Add serial architecture diagram -->

## Transmit and Receive

**Transmit:** All three interfaces transmit simultaneously. The UART TX signal is converted to RS-485, RS-232, and TTL levels in parallel. In practice, you connect the transmit terminal block of whichever interface your receiving device expects.

**Receive:** Only one interface can receive at a time, selected by the **RX SEL** hardware jumper:

| Position | Active Receive Interface |
|----------|------------------------|
| **N** | NMEA 0183 (RS-485) |
| **R** | RS-232 |
| **U** | UART |

Place the jumper on the pin pair corresponding to the interface you want to receive on.

!!! note
    RS-485 has separate TX and RX terminal blocks since it uses differential signaling with separate driver and receiver chips. RS-232 and UART each have TX and RX on a single 3-pin terminal block.

## Using Different Bit Rates for RX and TX

Normally, the same bit rate is used for transmit and receive. However, since UART0 is available (USB CDC handles the console), custom firmware could in principle assign UART0 to the TX pins and UART1 to the RX pins (or vice versa) via the ESP32-C3 GPIO matrix, allowing independent bit rates. For example, you could receive AIS at 38400 bit/s on RS-485 while transmitting NMEA 0183 at 4800 bit/s. This has not been tested.

## Interface Details

See the individual pages for wiring instructions and device-specific guidance:

- [NMEA 0183 (RS-485)](nmea-0183.md)
- [RS-232 Devices](rs-232.md)
- [UART Devices](uart.md)
