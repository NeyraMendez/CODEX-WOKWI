# Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a 4x4 matrix keypad and controls 12 LEDs based on key presses. The firmware logic is preserved from the provided source and organized into a clean repository layout with documentation-first structure.

## Features
- 4x4 keypad input scanning via `Keypad` library
- Direct LED control for keys `1..8` and `A..D`
- Group controls:
  - `9` = all blue LEDs ON
  - `0` = all blue LEDs OFF
  - `*` = all red LEDs ON
  - `#` = all red LEDs OFF
- Hardware documentation for Wokwi and real Pico W wiring

## Repository Structure

```text
.
├── CMakeLists.txt
├── README.md
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── include/
└── src/
    └── main.cpp
```

## Hardware Bill of Materials
- Raspberry Pi Pico W (RP2040)
- 4x4 membrane keypad
- 12 LEDs (8 blue + 4 red)
- 12 × 220Ω resistors (LED current limiting)
- 4 × 1kΩ resistors (keypad pull-ups)
- Breadboard/jumper wires

## GPIO Summary
See full mapping in [`docs/wiring.md`](docs/wiring.md).

- Keypad columns: GP19, GP18, GP17, GP16
- Keypad rows: GP26, GP22, GP21, GP20
- LED outputs: GP11, GP10, GP9, GP8, GP7, GP6, GP5, GP4, GP3, GP2, GP28, GP27

## Build and Flash (Pico SDK Layout)
> Note: The source logic uses Arduino APIs (`pinMode`, `digitalWrite`, `delay`, `Keypad`). Ensure your build/runtime provides Arduino compatibility for RP2040, or adapt the toolchain layer only.

1. Install Pico SDK prerequisites (if not already installed).
2. Configure SDK path:
   ```bash
   export PICO_SDK_PATH=/path/to/pico-sdk
   ```
3. Build:
   ```bash
   mkdir -p build
   cd build
   cmake ..
   make -j
   ```
4. Hold **BOOTSEL** on Pico W, connect USB, copy generated `.uf2` to the mass storage drive.

## Run in Wokwi
1. Create/open a Raspberry Pi Pico project in Wokwi.
2. Paste the provided `diagram.json` wiring.
3. Add this firmware source (`src/main.cpp`) in the simulator project.
4. Ensure the simulation environment includes the `Keypad` library and Arduino-style runtime support.
5. Start simulation and press keypad buttons to observe LED behavior.

## Run on Real Hardware
1. Wire exactly as documented in [`docs/wiring.md`](docs/wiring.md).
2. Build firmware for your selected RP2040 runtime that supports `Keypad`.
3. Flash UF2 to Pico W.
4. Validate key-to-LED behavior:
   - Press `1..8` for blue channel LEDs
   - Press `A..D` for red channel LEDs
   - Use `9/0/*/#` for bank operations

## Wi-Fi Notes
This firmware does **not** use Wi-Fi functionality, so no SSID/password or credential file is required.

## Documentation
- Wiring and pin map: [`docs/wiring.md`](docs/wiring.md)
- Firmware architecture: [`docs/architecture.md`](docs/architecture.md)
