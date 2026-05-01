# STM32 Self-Balancing Car (Kit Project)

A practical STM32 self-balancing robot car kit project for learning **PID control**, **IMU attitude sensing**, **encoder feedback**, and embedded robotics bring-up.

This README is written to be usable even when kit contents, board revisions, and firmware variants differ. Treat every checklist item as **“validate on your build”**.

---

## Project Status

- Hardware/bench validation: Not performed as part of this repo (no test claims)
- Firmware/feature support: Varies by kit and code revision; verify in your build
- Docs goal: Setup + PID tuning checklists with space for your notes

---

## What to Verify (box contents vs capabilities)

Different listings and revisions vary. Before you write “included” or “supported,” confirm with your actual kit and firmware.

### A) Box contents (hardware) — verify in your kit
Commonly listed items may include:
- STM32-based controller board (or STM32 MCU on a main board)
- Two-wheel chassis + hardware
- Encoder gear motors (or motors + separate encoders)
- IMU module (model varies)
- Ultrasonic distance module (optional)
- Battery holder / wiring (varies)

### B) Capabilities (features) — verify in your firmware/build
Listings sometimes mention:
- Balance PID control using IMU attitude estimation
- Encoder feedback usage
- App/remote control modes
- Ultrasonic obstacle behaviors (avoid/follow)

Treat these as **firmware-dependent** until verified.

---

## Repo Intent

This repo is meant to hold:
- Setup notes that are safe to follow without assuming hidden steps
- A PID calibration checklist with places to record results
- Optional placeholders for media/logs (only if you choose to add them)

If you add code or logs, keep them reproducible and avoid embedding sensitive data.

---

## Safety / Handling Notes

- Power off before changing wiring.
- Keep the robot lifted (wheels free) for first motor direction checks.
- Use a stable surface and clear space for first balancing attempts.
- Add output limits and a fast “motors off” control path before attempting balance.

---

## Setup Checklist (Bring-up)

### 1) Mechanical assembly (two-wheel chassis)
- [ ] Chassis assembled tightly (no looseness around motor mounts)
- [ ] Wheels installed and spin freely without rubbing
- [ ] IMU board and controller board are firmly mounted (no rotation relative to chassis)
- [ ] Center of mass roughly centered (battery placement consistent)

### 2) Wiring sanity checks
- [ ] IMU connected (orientation noted; “forward” direction marked)
- [ ] Encoder feedback connected for both motors (if your build has encoders)
- [ ] Ultrasonic module connected (only if present/used)
- [ ] Battery/power wired with correct polarity
- [ ] No cables can touch wheels during motion

Record here: IMU mounting orientation notes (text + optional photo filename)
- IMU notes:
- Photo filename (optional):

### 3) First power-on (no balancing yet)
- [ ] Power on with wheels off the ground
- [ ] Confirm motors can be commanded at low power
- [ ] Confirm encoder feedback changes when wheels are spun by hand (if present)
- [ ] Confirm IMU readings change when tilting the chassis (note sign/direction)

Record here:
- Motor A direction OK? (Y/N)
- Motor B direction OK? (Y/N)
- Encoder A changes with wheel spin? (Y/N/NA)
- Encoder B changes with wheel spin? (Y/N/NA)
- IMU tilt direction notes:

---

## PID Calibration Checklist (Practical, repeatable)

Goal: achieve stable balance using PID control based on IMU attitude sensing (and encoder feedback if your firmware uses it).

### A) Pre-tuning prerequisites
- [ ] IMU mounting orientation is known and consistent
- [ ] Encoders report consistent direction (forward vs backward) (if present/used)
- [ ] Motor directions are correct (forward command matches your definition of forward)
- [ ] Output limits are in place (max command, optional rate limit, fast disable)
- [ ] Power source is consistent for a tuning session (note the battery used)

### B) Data you should log each tuning attempt
Create a tuning log (file or spreadsheet) and record:
- Date/time:
- Surface (floor type):
- Power notes (battery type/voltage notes if available):
- IMU orientation note:
- Parameters:
  - Kp:
  - Ki:
  - Kd:
- Observed behavior (pick any that apply):
  - [ ] immediate fall
  - [ ] oscillation / shaking
  - [ ] slow drift
  - [ ] motor saturation (runs hard)
  - [ ] stable for ___ seconds (estimate)
- Notes / changes made:

### C) Stepwise tuning loop (repeatable workflow)
- [ ] Start with conservative parameters (record them)
- [ ] Make one change at a time, then retry
- [ ] If oscillation is strong, stop and reduce aggressiveness before continuing
- [ ] If it falls immediately, re-check IMU orientation and motor/encoder directions before increasing gains
- [ ] When it can balance briefly, iterate toward longer stability and smaller correction motion

### D) Encoder + speed feedback cross-check (optional)
- [ ] If encoder feedback is used, confirm both wheels respond similarly
- [ ] If one wheel consistently “runs away,” re-check encoder direction, wiring, and mechanical friction

---

## Ultrasonic Module Bring-up (Optional, if present/used)

Some kit listings mention ultrasonic-based behaviors; treat them as optional and firmware-dependent.

Checklist:
- [ ] Confirm the ultrasonic module is present and wired correctly
- [ ] Confirm your firmware actually reads it (no assumptions)
- [ ] Verify readings at short/medium distances with the robot stationary
- [ ] Only enable obstacle behaviors after balance is stable (avoid mixing causes)

Record here:
- Distance test notes:
- Any minimum/maximum stable reading:

---

## App / Remote Control Notes (Optional, if present/used)

Some kit listings mention app/remote control; treat it as optional and firmware-dependent.

Checklist:
- [ ] Confirm pairing/connection steps are documented locally (no hidden steps)
- [ ] Verify safe defaults (no unexpected full-speed motor command on connect)
- [ ] If the app can switch modes, document each mode and expected behavior
- [ ] Add a timeout/deadman behavior (return to neutral when commands stop)

Record here:
- App/controller used:
- Connection notes:
- Mode list + observations:

---

## Media and Logs (Optional)

If you choose to add media/logs for review or debugging, keep them clearly labeled and non-sensitive. Example filenames (adjust as needed):
- `media/bench-photo.jpg` — bench photo (if you took one)
- `media/balance-clip.mp4` — short balance attempt clip (if you recorded one)
- `tuning/tuning-log.csv` — tuning log spreadsheet export (if you keep one)
- `docs/wiring-notes.md` — wiring + orientation notes

---

## Suggested Repo Structure (Optional)

- `docs/` — setup notes, wiring photos, calibration notes
- `media/` — images/videos (only if you add them)
- `tuning/` — PID logs and experiment notes

---

## Related Links (Reference)

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial slug: `stm32-self-balancing-car-setup`
