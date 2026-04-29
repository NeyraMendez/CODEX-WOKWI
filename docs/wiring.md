# Wiring and GPIO Mapping

## Overview
This project connects a **4x4 matrix keypad** and **12 LEDs** to a Raspberry Pi Pico W. Each LED is driven from a dedicated GPIO pin through a 220Ω resistor. The keypad rows and columns are wired directly to GPIO pins, with pull-up resistors on row lines to 3.3V.

## Components (from `diagram.json`)
- 1x Raspberry Pi Pico / Pico W-compatible board
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8 blue LEDs (labels 1-8)
  - 4 red LEDs (labels A-D)
- 12x 220Ω resistors (LED current limiting)
- 4x 1kΩ resistors (keypad row pull-ups)
- Jumper wires and common GND rail

## Keypad GPIO Mapping
| Keypad Signal | Pico GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

### Row Pull-Ups
Each row line (R1-R4) is also tied to 3V3 through a 1kΩ resistor network (rp1-rp4 in the diagram).

## LED GPIO Mapping
The firmware array maps LEDs in this exact order:

| Firmware Index | Logical Label | Pico GPIO |
|---|---|---|
| ledPins[0] | 1 | GP11 |
| ledPins[1] | 2 | GP10 |
| ledPins[2] | 3 | GP9 |
| ledPins[3] | 4 | GP8 |
| ledPins[4] | 5 | GP7 |
| ledPins[5] | 6 | GP6 |
| ledPins[6] | 7 | GP5 |
| ledPins[7] | 8 | GP4 |
| ledPins[8] | A | GP3 |
| ledPins[9] | B | GP2 |
| ledPins[10] | C | GP28 |
| ledPins[11] | D | GP27 |

All LED cathodes are connected to GND.

## Serial Monitor
- GP0 -> Serial RX
- GP1 -> Serial TX

## Assumptions
- The provided Wokwi JSON uses `wokwi-pi-pico` but pinout is Pico W-compatible for this project.
- Keypad library scanning behavior depends on the runtime (Arduino core or compatible environment).
