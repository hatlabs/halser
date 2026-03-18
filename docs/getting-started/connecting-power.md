# Connecting Power and NMEA 2000

HALSER is powered through the 4-pin NMEA 2000 terminal block. The same connector provides both power and CAN bus connectivity.

## Powering via NMEA 2000

If you are connecting HALSER to an NMEA 2000 network, connect the four wires to the pluggable terminal block as follows:

<!-- TODO: Add photo of wired NMEA 2000 connector with labeled pins -->

| Pin | Signal | NMEA 2000 Color |
|-----|--------|-----------------|
| 1   | Shield | Bare / drain    |
| 2   | +12V   | Red             |
| 3   | GND    | Black           |
| 4   | CAN H  | White           |
| 5   | CAN L  | Blue            |

<!-- TODO: Verify pin numbering against actual board silkscreen -->

The board accepts 5–32 V input, matching the NMEA 2000 bus voltage range.

## Powering Without NMEA 2000

If you only need power (no CAN bus), connect your DC supply to the +12V and GND pins only. Any 5–32 V DC source is suitable.

<!-- TODO: Typical current consumption at 12V -->

## CAN Bus Termination

HALSER has a CAN termination resistor (120 Ω) that can be enabled via a solder jumper on the back of the board.

!!! warning "NMEA 2000 Networks"
    Do **not** enable the CAN termination resistor when connecting to a properly terminated NMEA 2000 network. NMEA 2000 networks have their own termination resistors at the backbone ends. Only enable HALSER's terminator if you are building a standalone CAN bus without external termination.

## Verifying Power

When power is applied, the **red power LED** lights up, indicating that the 3.3 V rail is active. If firmware is running on the ESP32-C3, the **RGB LED** also turns on — with the default firmware it shows a rainbow color cycle, confirming the microcontroller is operating correctly.
