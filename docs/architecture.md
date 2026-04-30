# Firmware Architecture

## Goal
Provide a maintainable project layout for a Pico W firmware that scans a 4x4 keypad and controls a 12-LED panel.

## Directory Design

- `src/main.py`
  - Program entrypoint.
  - Contains original control loop and business logic.
- `lib/`
  - Optional reusable modules (e.g., keypad scanner helpers, LED mapping helpers).
- `docs/wiring.md`
  - Hardware connectivity and GPIO truth table.
- `docs/architecture.md`
  - This architecture reference.

## Runtime Responsibilities (Typical)

1. **Pin Initialization**
   - Configure keypad row/column GPIO direction.
   - Configure LED pins as outputs.
2. **Input Scan**
   - Scan keypad matrix (drive/read pattern) with debouncing.
3. **Decision Logic**
   - Map pressed keys to output states.
4. **Output Update**
   - Set LED states based on logic.
5. **Telemetry/Debug (Optional)**
   - Print serial diagnostics over GP0/GP1 in Wokwi setup.

## Suggested Module Boundaries (No Behavior Change)

If refactoring becomes necessary later (still preserving behavior):
- `lib/keypad.py`: row/column scan routine and key decode map.
- `lib/led_panel.py`: LED label-to-GPIO mapping and output write helpers.
- `src/main.py`: orchestration only.

## Wi-Fi Considerations (Pico W)

If Wi-Fi is present in firmware logic:
- Keep credentials out of source control via local `secrets.py`.
- Add reconnection/backoff strategy in runtime loop (future enhancement only).
- Do not block keypad/LED timing with long network operations.

## Compatibility Notes

- Documentation targets **Raspberry Pi Pico W** pin compatibility.
- The provided Wokwi part is `wokwi-pi-pico`; GPIO mapping is compatible for this digital I/O use case.
