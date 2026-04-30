# Raspberry Pi Pico W Keypad + LED Panel (Wokwi)

## Project Overview
This repository documents a Raspberry Pi Pico W project modeled in Wokwi with:
- A 4x4 membrane keypad used as digital input.
- A 12-LED output panel (8 blue LEDs labeled `1..8`, 4 red LEDs labeled `A..D`).
- Pull-up resistor network for keypad row lines.

> **Important:** The source firmware body was not included in the provided input (`main.py` content was empty), so this repository focuses on clean structure and hardware/software documentation **without changing runtime logic**.

## Repository Structure (MicroPython-oriented)

```
.
├── src/
│   └── main.py
├── lib/
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── diagram.json
└── README.md
```

- `src/main.py`: Main firmware entrypoint placeholder (keep your original logic here).
- `lib/`: Optional reusable drivers/helpers.
- `docs/wiring.md`: Hardware wiring details and GPIO map.
- `docs/architecture.md`: Runtime architecture and module-level responsibilities.
- `diagram.json`: Wokwi hardware definition.

## Hardware Components (from `diagram.json`)
- 1x Raspberry Pi Pico (project target is Pico W-compatible pinout)
- 1x 4x4 membrane keypad
- 12x LEDs total:
  - 8x blue LEDs (`1..8`)
  - 4x red LEDs (`A..D`)
- 12x current-limit resistors for LEDs (`220Ω` each)
- 4x pull-up resistors for keypad row lines (`1kΩ` each)

## GPIO Allocation Summary

### Keypad
- Columns:
  - C4 -> GP16
  - C3 -> GP17
  - C2 -> GP18
  - C1 -> GP19
- Rows:
  - R4 -> GP20
  - R3 -> GP21
  - R2 -> GP22
  - R1 -> GP26
- Additional pull-ups to 3V3 on rows R1-R4 (via 1kΩ network).

### LED Outputs
- Blue LEDs:
  - `8` -> GP4
  - `7` -> GP5
  - `6` -> GP6
  - `5` -> GP7
  - `4` -> GP8
  - `3` -> GP9
  - `2` -> GP10
  - `1` -> GP11
- Red LEDs:
  - `A` -> GP3
  - `B` -> GP2
  - `C` -> GP28
  - `D` -> GP27
- All LED cathodes are tied to GND.

## Notes About the Student Hardware Description
The textual “student interpretation” references an **I2C LCD1602** and a **DHT22 on GP15**. Those components/pins are **not present** in the provided `diagram.json`.

This documentation therefore treats `diagram.json` as the source of truth. If your actual firmware uses LCD/DHT22/Wi-Fi, update `docs/architecture.md` and `docs/wiring.md` accordingly.

## Running in Wokwi
1. Open [wokwi.com](https://wokwi.com/).
2. Create/import a Raspberry Pi Pico project.
3. Replace the project `diagram.json` with this repository’s `diagram.json`.
4. Place your MicroPython firmware logic in `src/main.py`.
5. Start simulation and observe serial output and LED behavior.

## Running on Real Pico W Hardware
1. Install MicroPython UF2 for Pico W (if not already flashed).
2. Copy `src/main.py` to the board root as `main.py`.
3. Copy any helper modules from `lib/`.
4. Wire keypad and LEDs exactly as documented in `docs/wiring.md`.
5. Power cycle/reset the board to execute `main.py`.

## Wi-Fi & Credentials Safety
If your firmware uses Wi-Fi:
- Store SSID/password in a separate local file (e.g., `secrets.py`) that is **not committed**.
- Example pattern:
  - `secrets.py`:
    ```python
    WIFI_SSID = "..."
    WIFI_PASSWORD = "..."
    ```
  - `main.py` imports these constants at runtime.
- Keep `secrets.py` in `.gitignore`.

