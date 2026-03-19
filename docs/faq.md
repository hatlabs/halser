# FAQ

## Can I use multiple serial interfaces at the same time?

Only **one** serial interface can receive data at a time. The active receive interface is selected in firmware (RS-485 RX by default). All interfaces transmit the same signal simultaneously.

## Which serial interface is active by default?

The active receive interface is selected by the **RX SEL** hardware jumper on the board. Set it to **N** for NMEA 0183 (RS-485), **R** for RS-232, or **U** for UART.

## What bit rate does HALSER use?

The default firmware uses 4800 bit/s (standard NMEA 0183). This is configurable via the web UI. AIS devices typically require 38400 bit/s.

## Can I use HALSER without an NMEA 2000 network?

Yes. HALSER can operate as a WiFi-only device with Signal K output. You still need to provide 5–32 V power through the NMEA 2000 connector's power pins (CAN bus wires are optional).

## Does HALSER support Bluetooth?

No. The ESP32-C3 chip supports BLE, but HALSER's firmware and antenna design focus on WiFi. Bluetooth is not exposed or supported.

## Can I write my own firmware?

Yes — that is the intended use. HALSER is a development board. See [Custom Firmware Development](software/custom-firmware.md) for details on setting up a development environment and building firmware.

## Does the default firmware support AIS?

No. The default firmware only parses six NMEA 0183 sentence types (GGA, RMC, VTG, HDG, VHW, DPT, MWV). AIS sentences (VDM, VDO) are silently ignored. Bridging AIS data requires [custom firmware](software/custom-firmware.md).

## Is HALSER a bidirectional gateway?

The default firmware is one-directional: NMEA 0183 → NMEA 2000 only. Bidirectional translation (N2K → 0183) would require custom firmware.

## How do I reset the WiFi settings?

<!-- TODO: Document the WiFi reset procedure -->

## Can I use Victron VE.Direct with HALSER?

<!-- TODO: Verify VE.Direct compatibility -->

Victron VE.Direct uses raw UART at 19200 bit/s. It should be possible to connect a VE.Direct cable to HALSER's UART port (3.3 V jumper setting) and parse the VE.Direct protocol in custom firmware. This is not supported by the default firmware.
