# Default Firmware

HALSER ships with a pre-installed NMEA 0183 → NMEA 2000 gateway firmware. It is provided for quick evaluation and as a reference for custom firmware development. The source code is available at [hatlabs/HALSER-default-firmware](https://github.com/hatlabs/HALSER-default-firmware).

## What It Does

The default firmware reads NMEA 0183 sentences from the RS-485 RX interface and translates them to NMEA 2000 messages on the CAN bus. It also provides WiFi connectivity with a web UI for configuration and Signal K output.

## NMEA 0183 → NMEA 2000 Translation

| NMEA 0183 Input | N2K PGN | Description | Transmit Rate |
|-----------------|---------|-------------|---------------|
| GGA + RMC | 129029 | GNSS Position Data | 1000 ms |
| RMC + VTG | 129026 | COG & SOG, Rapid Update | 250 ms |
| HDG | 127250 | Vessel Heading | 100 ms |
| VHW | 128259 | Speed, Water Referenced | 1000 ms |
| DPT | 128267 | Water Depth | 1000 ms |
| MWV | 130306 | Wind Data | 1000 ms |

Only the sentence types listed above are processed. All other NMEA 0183 sentences are silently ignored.

### Value Expiry

If no update is received for a particular value within approximately 5 seconds, the corresponding NMEA 2000 message stops being transmitted. This prevents stale data from persisting on the network.

## WiFi

On first boot, the firmware creates a WiFi access point:

<!-- TODO: Confirm default SSID, password, and IP address -->

- **SSID:** `halser-XXXXXX` (where XXXXXX is derived from the MAC address)
- **IP address:** TODO

Connect to the access point and open the web UI in a browser to configure WiFi client mode and other settings.

## Web UI

The SensESP web UI provides:

<!-- TODO: Add screenshots of the web UI -->

- **WiFi configuration** — Connect to an existing network
- **NMEA 0183 baud rate** — Default 4800 baud, configurable (requires restart)
- **Signal K connection** — Configure Signal K server address
- **Device info** — Firmware version, hostname, network status
- **OTA update** — Upload new firmware over WiFi

## NMEA 2000 Device Identity

| Field | Value |
|-------|-------|
| Manufacturer | Hat Labs (code 2046) |
| Product code | 100 |
| Model ID | HALSER NMEA 0183-N2K GW |
| Device class | 25 (Inter/Intranetwork Device) |
| Device function | 130 (PC Gateway) |
| Serial number | Derived from WiFi MAC address |

## RGB LED Behavior

- **Rainbow color cycle** — Running, waiting for data
- **Brief off-blink** — NMEA 0183 sentence received (50 ms off per sentence)

## Limitations

- Only handles the six NMEA 0183 sentence types listed above
- Receives on whichever interface is selected by the RX SEL hardware jumper
- One-directional: NMEA 0183 → NMEA 2000 only (no N2K → 0183 translation)
- No AIS sentence support (VDM/VDO are ignored)

For use cases not covered by the default firmware, see [Custom Firmware Development](custom-firmware.md).
