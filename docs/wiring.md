# Wiring Guide (Raspberry Pi Pico W)

## Scope
This wiring map is derived directly from the provided Wokwi `diagram.json`.
When diagram and prose differ, this file follows the diagram.

## Components
- Raspberry Pi Pico / Pico W-compatible pinout
- 4x4 membrane keypad (`R1..R4`, `C1..C4`)
- 12x LEDs (`1..8`, `A..D`)
- 12x 220Ω resistors (one per LED anode path)
- 4x 1kΩ resistors as pull-ups for keypad rows

## GPIO Pin Mapping

| Function | Device Pin | Pico W GPIO | Electrical Note |
|---|---|---:|---|
| Keypad Column 4 | C4 | GP16 | Digital I/O |
| Keypad Column 3 | C3 | GP17 | Digital I/O |
| Keypad Column 2 | C2 | GP18 | Digital I/O |
| Keypad Column 1 | C1 | GP19 | Digital I/O |
| Keypad Row 4 | R4 | GP20 | Pulled up to 3V3 via 1kΩ |
| Keypad Row 3 | R3 | GP21 | Pulled up to 3V3 via 1kΩ |
| Keypad Row 2 | R2 | GP22 | Pulled up to 3V3 via 1kΩ |
| Keypad Row 1 | R1 | GP26 | Pulled up to 3V3 via 1kΩ |
| LED `8` | Anode | GP4 | Series 220Ω |
| LED `7` | Anode | GP5 | Series 220Ω |
| LED `6` | Anode | GP6 | Series 220Ω |
| LED `5` | Anode | GP7 | Series 220Ω |
| LED `4` | Anode | GP8 | Series 220Ω |
| LED `3` | Anode | GP9 | Series 220Ω |
| LED `2` | Anode | GP10 | Series 220Ω |
| LED `1` | Anode | GP11 | Series 220Ω |
| LED `A` | Anode | GP3 | Series 220Ω |
| LED `B` | Anode | GP2 | Series 220Ω |
| LED `C` | Anode | GP28 | Series 220Ω |
| LED `D` | Anode | GP27 | Series 220Ω |

All LED cathodes connect to Pico GND.

## Power Topology
- Keypad pull-up network is tied to `3V3`.
- LED return path is tied to `GND`.

## Serial
- `GP0` -> Serial RX monitor
- `GP1` -> Serial TX monitor

These are used by Wokwi serial monitor in the supplied diagram.

## Assumptions / Clarifications
- No LCD1602 or DHT22 is connected in the provided diagram.
- If your actual hardware includes those devices, add a supplemental wiring section and preserve existing pin mappings if already used by firmware.
