# Arduino Firmware — `Sketch_mech_CAN`

Arduino sketch that reads OBD-II PIDs from the vehicle over the CAN bus and forwards them to the Android app over Bluetooth.

## Hardware

- Arduino (Uno or equivalent)
- SeeedStudio CAN-Bus Shield (or compatible MCP2515-based shield)
- OBD-II cable (DB9 → OBD-II)
- HC-06 Bluetooth module
  - TX → Arduino pin 4
  - RX → Arduino pin 5
  - Default baud: `57600`

## Build

1. Install the [Mechanic library](../libraries/mechanic-0.6.zip) into your Arduino IDE *(Sketch → Include Library → Add .ZIP Library)*.
2. Open `Sketch_mech_CAN/Sketch_mech_CAN.ino`.
3. Select your board, then **Upload**.

> Works with vehicles model year 2008 and newer (post-CAN OBD-II mandate).

## Protocol

A single character is sent from the Android app to indicate the active page; the sketch responds accordingly.

| Page char | Meaning | Sketch behavior |
|-----------|---------|-----------------|
| `m` | Main menu | Reports whether the CAN-Bus link is alive |
| `d` | Dashboard | Streams speed, RPM, fuel %, throttle %, and battery voltage at the requested refresh rate |
| `c` | Diagnostics | Issues a DTC request and returns the trouble codes |

Each dashboard payload is prefixed with a 4-character tag identifying the field so dropped Bluetooth characters do not corrupt the parse on the Android side.

## Files

- [`Sketch_mech_CAN/Sketch_mech_CAN.ino`](Sketch_mech_CAN/Sketch_mech_CAN.ino) — main sketch
