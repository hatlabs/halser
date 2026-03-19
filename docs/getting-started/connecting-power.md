# Connecting Power and NMEA 2000

HALSER is powered through the 4-pin NMEA 2000 terminal block. The same connector provides both power and CAN bus connectivity.

## Powering via NMEA 2000

If you are connecting HALSER to an NMEA 2000 network, connect the four wires to the pluggable terminal block as follows:

<!-- TODO: Add photo of wired NMEA 2000 connector with labeled pins -->

| Pin | Signal | NMEA 2000 Color |
|-----|--------|-----------------|
| 1   | GND    | Black           |
| 2   | Vin    | Red             |
| 3   | CAN H  | White           |
| 4   | CAN L  | Blue            |

The NMEA 2000 bus voltage is nominally 12 V. HALSER's power input accepts 5–32 V, so it works directly on the bus.

!!! note "NMEA 2000 Shield"
    Per the NMEA 2000 standard, the cable shield (bare/drain wire) must be left unconnected at device ends. Only connect the shield at the designated grounding point on the NMEA 2000 backbone.

## Powering Without NMEA 2000

If you only need power (no CAN bus), connect your DC supply to pins 1 (GND) and 2 (Vin) only. Any 5–32 V DC source is suitable.

<!-- TODO: Typical current consumption at 12V -->


## Verifying Power

When power is applied, the **red power LED** lights up, indicating that the 3.3 V rail is active. If firmware is running on the ESP32-C3, the **RGB LED** also turns on — with the default firmware it shows a rainbow color cycle, confirming the microcontroller is operating correctly.
