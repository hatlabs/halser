# Custom Firmware Development

This guide covers setting up a development environment and building custom firmware for HALSER.

## Development Environment

HALSER firmware is developed using [PlatformIO](https://platformio.org/) with the Arduino framework. PlatformIO integrates with VS Code and provides dependency management, build automation, and device upload.

### Platform Configuration

Use the following `platformio.ini` configuration as a starting point:

```ini
[env:esp32-c3]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/54.03.20/platform-espressif32.zip
board = esp32-c3-devkitm-1
framework = arduino
lib_ldf_mode = deep
upload_speed = 2000000
monitor_speed = 115200
build_flags =
    -DARDUINO_USB_CDC_ON_BOOT=1
    -DARDUINO_USB_MODE=1
```

!!! note "USB CDC"
    The `ARDUINO_USB_CDC_ON_BOOT=1` flag is required for USB serial communication on the ESP32-C3. Without it, `Serial` output will not appear over USB.

## Pin Assignments

Always use the HALSER pin definitions rather than hard-coded GPIO numbers. See the [GPIO Reference](../hardware/hardware.md#gpio-reference) for the complete mapping.

Key pins for serial communication:

| Function | GPIO | Constant (default firmware) |
|----------|------|-----------------------------|
| UART1 TX | 2 | `kUART1TxPin` |
| UART1 RX | 3 | `kUART1RxPin` |
| CAN TX | 4 | `kCANTxPin` |
| CAN RX | 5 | `kCANRxPin` |
| I2C SDA | 6 | `kI2CSDA` |
| I2C SCL | 7 | `kI2CSCL` |
| RGB LED | 8 | `kRGBLEDPin` |
| Button | 9 | `kButtonPin` |
| 1-Wire | 10 | `kOneWirePin` |

## Key Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| [SensESP](https://github.com/SignalK/SensESP) | 3.2.0 | IoT framework (WiFi, web UI, Signal K) |
| [SensESP/NMEA0183](https://github.com/SignalK/SensESP) | — | NMEA 0183 sentence parsing |
| [NMEA2000-library](https://github.com/ttlappalainen/NMEA2000) | 4.17.2 | NMEA 2000 message handling |
| [NMEA2000_twai](https://github.com/ttlappalainen/NMEA2000_twai) | — | ESP32 TWAI (CAN) driver for NMEA2000 |
| [Adafruit NeoPixel](https://github.com/adafruit/Adafruit_NeoPixel) | — | RGB LED control |

## Starting Points

### From the Default Firmware

The [HALSER default firmware](https://github.com/hatlabs/HALSER-default-firmware) provides a complete working example of:

- SensESP application setup
- NMEA 0183 sentence parsing (GGA, RMC, VTG, HDG, VHW, DPT, MWV)
- NMEA 2000 message transmission
- RGB LED status indication
- Configurable bit rate via web UI

Clone and modify it to suit your needs.

### From a SensESP Template

For a fresh start, use the [SensESP project template](https://github.com/SignalK/SensESP/tree/main/examples) and add HALSER-specific pin definitions.

### Bare Arduino

For minimal projects that don't need WiFi or web UI:

```cpp
#include <Arduino.h>

// HALSER pin definitions
constexpr int kUART1TxPin = 2;
constexpr int kUART1RxPin = 3;
constexpr int kCANTxPin = 4;
constexpr int kCANRxPin = 5;
constexpr int kRGBLEDPin = 8;
constexpr int kButtonPin = 9;
constexpr int kOneWirePin = 10;

void setup() {
    Serial.begin(115200);  // USB CDC serial
    Serial1.begin(4800, SERIAL_8N1, kUART1RxPin, kUART1TxPin);
}

void loop() {
    // Read from NMEA 0183 input
    while (Serial1.available()) {
        char c = Serial1.read();
        Serial.print(c);  // Echo to USB for debugging
    }
}
```

## Example Projects

These ready-to-use firmware projects demonstrate what you can build with HALSER. Each is a complete SensESP application with WiFi, web UI, Signal K output, NMEA 2000 integration, and OTA updates.

### Wind Instrument Gateway

Bridges an [Autonnic A5120](https://autonnic.com/a5120/) ultrasonic wind instrument to NMEA 2000 and Signal K. Receives apparent wind data via NMEA 0183 at 4800 bit/s (RS-232) and transmits PGN 130306 (Wind Data) on the NMEA 2000 bus. Sensor parameters (reference angle, damping, repetition rate) are configurable via the web UI. Optional OLED display shows live wind speed and angle.

Source code and full documentation: [HALSER Wind Interface on GitHub](https://github.com/hatlabs/HALSER-wind-interface)

### AIS Transponder Gateway

Bridges a [Matsutec HA-102](http://www.matsutec.com.cn/) AIS transponder to NMEA 2000 and Signal K. Decodes AIS messages (Class A/B position reports, static data, safety messages, Aids to Navigation) received via NMEA 0183 at 38400 bit/s (RS-232) and forwards them as standard NMEA 2000 PGNs. The transponder's MMSI, static ship data, and voyage data are configurable via the web UI. Supports receive-only mode, bidirectional Signal K sync for voyage data, and optional OLED display.

Source code and full documentation: [HALSER AIS Interface on GitHub](https://github.com/hatlabs/HALSER-ais-interface)

## Project Ideas

These are conceptual starting points — no ready-made firmware exists for them yet.

### Victron VE.Direct Integration

<!-- TODO: Verify VE.Direct compatibility -->

Victron VE.Direct uses raw UART at 19200 bit/s. Connect the VE.Direct cable to the UART terminal block (3.3 V jumper setting) and parse the VE.Direct text protocol in firmware.

## Programming

### USB-C Upload

Connect HALSER to your computer via USB-C. PlatformIO will detect the ESP32-C3 USB CDC serial port automatically.

```bash
# Build and upload
pio run -t upload

# Monitor serial output
pio device monitor
```

### OTA Updates

If using SensESP, over-the-air (OTA) firmware updates are supported via the web UI once WiFi is configured.
