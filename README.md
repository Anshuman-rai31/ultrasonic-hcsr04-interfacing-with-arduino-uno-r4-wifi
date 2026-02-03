# Ultrasonic Distance Sensor — Arduino Uno R4 WiFi

## Overview
Simple Arduino project that reads distance from an HC\-SR04 ultrasonic sensor and prints the result to the Serial Monitor. Main code is in `src/main.cpp`. Build and upload using PlatformIO configured by `platformio.ini`.

## Hardware
- Arduino Uno R4 WiFi
- HC\-SR04 ultrasonic sensor
- Jumper wires
- Breadboard (optional)
- USB cable

## Wiring
- HC\-SR04 VCC -> Arduino 5V
- HC\-SR04 GND -> Arduino GND
- HC\-SR04 TRIG -> Arduino digital pin 9 (`trigPin`)
- HC\-SR04 ECHO -> Arduino digital pin 10 (`echoPin`)

Note: Ensure the ECHO voltage is safe for the board (HC\-SR04 is 5V; Uno R4 WiFi accepts 5V).

## Files
- `src/main.cpp` — Arduino sketch that triggers the sensor, measures echo with `pulseIn`, calculates distance, and prints to Serial.
- `platformio.ini` — PlatformIO project configuration for the Uno R4 WiFi board.

## PlatformIO (`platformio.ini`) — example notes
Ensure `platformio.ini` selects a compatible platform and board (Uno R4 WiFi). Typical entries:
- `platform` matching Espressif/Arduino framework as appropriate
- `board` set to the Uno R4 WiFi identifier
- `framework = arduino`

(See your existing `platformio.ini` for exact values.)

## Usage
1. Connect hardware as described.
2. Open the project in PlatformIO and upload to `Arduino Uno R4 WiFi`.
3. Open Serial Monitor at `9600` baud.
4. Observe distance readings (cm) updating roughly once per second.

## Troubleshooting
- No or erratic readings:
  - Verify wiring and common GND.
  - Ensure TRIG is configured as OUTPUT and ECHO as INPUT in `src/main.cpp`.
  - Add a timeout to `pulseIn` to avoid indefinite blocking if no echo is received.
- Readings too large or zero:
  - Confirm sensor faces an object within range (~2 cm to 400 cm).
  - Check stable 5V supply.

## Notes
- Distance calculation uses speed of sound ≈ 0.034 cm/µs (duration × 0.034 / 2).
- Current sketch uses blocking `pulseIn` and `delay`. For higher performance or non\-blocking behaviour consider timers or interrupts.

## License
MIT (include `LICENSE` in project root if needed)
