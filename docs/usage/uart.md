# UART Devices

The UART interface provides TTL-level serial communication for devices that output raw UART signals. This is common on bare sensor modules, microcontroller boards, and some consumer devices.

## Wiring

<!-- TODO: Add wiring diagram for UART -->
<!-- TODO: Add photo of wired UART connector -->

Connect the device to the UART 3-pin terminal block:

| Pin | Signal | Description |
|-----|--------|-------------|
| 1   | TX     | HALSER transmit → device receive |
| 2   | RX     | Device transmit → HALSER receive |
| 3   | GND    | Signal ground |

<!-- TODO: Verify pin ordering against board silkscreen -->

## Voltage Selection

The UART output voltage can be set to **3.3 V or 5 V** using a jumper on the board.

<!-- TODO: Add photo showing jumper location and positions -->

- **3.3 V** — For 3.3 V logic devices (most modern modules)
- **5 V** — For 5 V logic devices (Arduino Uno, classic sensors)

The UART input is **5 V tolerant** regardless of the jumper setting.

## Compatible Devices

The UART interface is suitable for:

- **Victron VE.Direct** — Raw UART at 19200 bit/s. Connect the VE.Direct cable's TX, RX, and GND wires directly to the UART terminal block. Set the jumper to 3.3 V.
- **Serial sensors** — Sensors with UART I/O requiring galvanic isolation
- **Microcontroller-to-microcontroller** — Direct communication with Arduino, ESP32, or other MCU boards when isolation is required
