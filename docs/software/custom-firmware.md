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
- Configurable baud rate via web UI

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

## Example Use Cases

### AIS Receiver Bridge

The default firmware does not handle AIS sentences (VDM/VDO). To bridge AIS data, you need custom firmware that:

1. Receives NMEA 0183 on RS-485 RX at 38400 baud
2. Parses or forwards VDM/VDO sentences
3. Sends data via WiFi (Signal K, TCP, or UDP)

<!-- TODO: Link to example AIS firmware or provide more detailed guidance -->

### 1-Wire Temperature Sensor to NMEA 2000

Connect a DS18B20 temperature sensor to the 1-Wire header and transmit PGN 130312 (Temperature) on the NMEA 2000 bus. The SensESP framework has built-in support for both 1-Wire sensors and NMEA 2000 temperature messages.

### Victron VE.Direct Integration

<!-- TODO: Verify VE.Direct compatibility -->

Victron VE.Direct uses raw UART at 19200 baud. Connect the VE.Direct cable to the UART terminal block (3.3 V jumper setting) and parse the VE.Direct text protocol in firmware.

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
