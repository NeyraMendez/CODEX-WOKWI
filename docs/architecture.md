# Firmware Architecture

## High-Level Design
The firmware is a single-module event loop:
1. Initialize all LED GPIO pins as outputs and force OFF state in `setup()`.
2. Poll keypad state in `loop()` with `keypad.getKey()`.
3. If a key is pressed, execute a `switch` action that turns on/off one LED or a group of LEDs.
4. Delay 10ms for scan pacing.

## Source Layout
- `src/main.cpp`: Core firmware logic (unchanged behavior from provided source).
- `include/`: Reserved for future headers/extensions.
- `docs/wiring.md`: Hardware connectivity and GPIO map.
- `docs/architecture.md`: This design overview.

## Input/Output Behavior
### Inputs
- Keypad keys: `0-9`, `A-D`, `*`, `#`.

### Outputs
- 12 individual LEDs mapped in `ledPins[]`.

### Action Map
- `1..8`: Turn ON corresponding blue LED.
- `9`: Turn ON blue LED bank (indices `0..7`).
- `0`: Turn OFF blue LED bank (indices `0..7`).
- `A..D`: Turn ON corresponding red LED.
- `*`: Turn ON red LED bank (indices `8..11`).
- `#`: Turn OFF red LED bank (indices `8..11`).

## Non-Functional Notes
- No Wi-Fi APIs are used even though target is Pico W.
- No credential handling required.
- Logic is intentionally preserved as-is; there is no state reset on single-key ON events except via bank OFF keys (`0` and `#`).
