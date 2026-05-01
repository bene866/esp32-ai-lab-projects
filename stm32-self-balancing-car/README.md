# STM32 Self-Balancing Car (Kit Project)

A hands-on STM32 self-balancing robot car kit project for learning **PID control**, **IMU attitude sensing**, **encoder motor feedback**, and embedded robotics experiments. This README is written as a **review-required draft** and focuses on a practical **setup + PID calibration checklist**.

---

## Validation Status (as of 2026-04-30)

- Hardware validation: **Not verified in this repo run** (no claims of completed bench tests)
- Documentation status: **Draft checklist** for human review
- What to validate before publishing: assembly photos, wiring notes, firmware build steps, tuning logs, and demo media files

---

## What’s Included (kit-level)

From the kit description:

- STM32-based self-balancing robot car kit
- Two-wheel balancing chassis
- IMU attitude sensing module
- Encoder gear motors
- Ultrasonic module
- Battery holder and wiring
- Source code and learning materials
- App control support
- Ultrasonic obstacle avoidance / following function

---

## Repo Intent

This repo is meant to hold:

- Setup notes that are **safe to follow** without assuming hidden steps
- A **PID calibration checklist** with places to record results
- Demo media placeholders (so reviewers can see what is still missing)

If you add code, keep it reproducible and avoid embedding any sensitive data.

---

## Safety / Handling Notes

- Power off before changing wiring.
- Keep the robot lifted (wheels free) for first motor direction checks.
- Use a stable surface and clear space for first balancing attempts.

---

## Setup Checklist (Bring-up)

### 1) Mechanical assembly (two-wheel chassis)
- [ ] Chassis assembled tightly (no looseness around motor mounts)
- [ ] Wheels installed and spin freely without rubbing
- [ ] Center of mass roughly centered (battery placement consistent)

### 2) Wiring sanity checks
- [ ] IMU module connected (orientation noted: “forward” direction marked)
- [ ] Encoder motor feedback connected for both motors
- [ ] Ultrasonic module connected (if used in your build)
- [ ] Battery holder wired with correct polarity
- [ ] No cables can touch wheels during motion

> Record here: IMU mounting orientation notes (text + photo filename):
- IMU notes:
- Photo:

### 3) First power-on (no balancing yet)
- [ ] Power on with wheels off the ground
- [ ] Confirm motors can be commanded without unexpected direction
- [ ] Confirm encoder feedback changes when wheels are spun by hand
- [ ] Confirm IMU readings change when tilting the chassis (sign/direction noted)

> Record here:
- Motor A direction OK? (Y/N)
- Motor B direction OK? (Y/N)
- Encoder A changes with wheel spin? (Y/N)
- Encoder B changes with wheel spin? (Y/N)
- IMU tilt direction notes:

---

## PID Calibration Checklist (Practical, repeatable)

Goal: achieve stable balance using **PID control** with IMU attitude sensing and encoder feedback.

### A) Pre-tuning prerequisites
- [ ] IMU mounting orientation is known and consistent
- [ ] Encoders report consistent direction (forward vs backward)
- [ ] Motor directions are correct (forward command moves the robot forward)
- [ ] Battery voltage is consistent for a tuning session (note the battery used)

### B) Data you should log each tuning attempt
Create a simple tuning log (file or spreadsheet) and record:

- Date/time:
- Surface (floor type):
- Battery / power notes:
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
  - [ ] stable for ___ seconds
- Notes / changes made:

### C) Stepwise tuning loop (repeatable workflow)
- [ ] Start with conservative parameters (record them; do not guess later)
- [ ] Make **one change at a time**, then retry
- [ ] If oscillation is strong, stop and reduce aggressiveness before continuing
- [ ] If it falls immediately, re-check IMU orientation and motor directions before increasing gains
- [ ] When it can balance briefly, iterate toward longer stability and smaller correction motion

### D) Encoder + speed feedback cross-check (optional but recommended)
- [ ] If encoder feedback is used for motor control, confirm both wheels respond similarly
- [ ] If one wheel consistently “runs away,” re-check encoder direction, wiring, and mechanical friction

---

## Ultrasonic Module Bring-up (if used)

Supported feature (kit-level): ultrasonic obstacle avoidance / following function.

Checklist:
- [ ] Confirm the ultrasonic module is detected/used by your firmware (no assumptions)
- [ ] Verify readings at short/medium distances with the robot stationary
- [ ] Only enable obstacle behaviors after balance is stable (to avoid mixing causes)

> Record here:
- Distance test notes:
- Any minimum/maximum stable reading:

---

## App Control Notes (if used)

Supported feature (kit-level): app control support.

Checklist:
- [ ] Confirm pairing/connection steps are documented locally (no hidden steps)
- [ ] Verify safe defaults (no unexpected full-speed motor command on connect)
- [ ] If the app can switch modes, document each mode and expected behavior

> Record here:
- App used:
- Connection notes:
- Mode list + observations:

---

## Demo Media (Placeholders)

Add real files and update names/paths here once available:

- `media/bench-photo.jpg` — kit bench photo
- `media/balance-first-success.mp4` — first stable balance clip
- `media/pid-oscillation-example.mp4` — example failure mode (useful for debugging)
- `media/app-control-demo.mp4` — app control behavior (if applicable)
- `media/ultrasonic-demo.mp4` — obstacle avoidance/following demo (if applicable)

---

## Recommended Repo Additions (Non-secret)

If you’re organizing this project, these folders make review easier:

- `docs/` — setup notes, wiring photos, calibration notes
- `media/` — images/videos listed above
- `tuning/` — PID logs and experiment notes

---

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial topic: **STM32 self-balancing car setup and PID calibration checklist**
- Planned tutorial slug: `stm32-self-balancing-car-setup`
