# Software Overview

HALSER is a development board. While it ships with a basic default firmware for evaluation, most users will develop custom firmware tailored to their specific application.

## Development Options

Several frameworks are available for HALSER firmware development:

### SensESP (Recommended)

[SensESP](https://signalk.org/SensESP/) is an IoT sensor framework for ESP32 that provides WiFi connectivity, a web-based configuration UI, Signal K integration, and NMEA 2000 support out of the box. It is the recommended starting point for most HALSER applications.

The [HALSER default firmware](https://github.com/hatlabs/HALSER-default-firmware) is built on SensESP and serves as a good reference for custom projects.

### Arduino

The Arduino framework for ESP32 provides a familiar development environment with access to a vast library ecosystem. Use this if you prefer the Arduino API or need specific Arduino-compatible libraries.

### ESP-IDF

Espressif's official IoT Development Framework offers the most control and performance. Suitable for advanced use cases that require fine-grained hardware control or real-time guarantees.

### ESPHome

[ESPHome](https://esphome.io/) is a configuration-based approach to ESP32 firmware. It is well suited for home automation integration and simple sensor applications, though it has more limited support for marine-specific protocols.

## Pin Assignments

HALSER's GPIO pin assignments differ from generic ESP32-C3 development kits. Always refer to the [GPIO Reference](../hardware/hardware.md#gpio-reference) when developing firmware.

## Default Firmware

HALSER ships with a pre-installed [default firmware](default-firmware.md) that acts as an NMEA 0183 → NMEA 2000 gateway. It is provided for quick evaluation and as a development reference — see [Default Firmware](default-firmware.md) for details.

## Getting Started with Development

See [Custom Firmware Development](custom-firmware.md) for a guide to setting up your development environment and building firmware for HALSER.
