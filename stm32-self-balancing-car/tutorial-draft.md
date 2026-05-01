---
status: publish
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: false
publish_target: WordPress
---

# STM32 self-balancing car kit setup + PID calibration checklist

A practical, hardware/firmware-agnostic checklist for bringing up a **two-wheel STM32 self-balancing robot car** and tuning PID control. It avoids assuming any specific IMU model, motor driver, pin map, or “known-good” gains.

If your kit, board revision, or firmware differs from what this checklist expects, treat each step as **“validate on your build”** and adjust accordingly.

## What to verify from your actual kit (reference, not a promise)

Different sellers and revisions vary. Before you document anything as “included” or “supported,” verify against what you physically have and what your firmware actually does.

### Box contents (hardware) — verify in your kit
Your kit may include items like:
- STM32-based controller board (or STM32 MCU on a main board)
- Two-wheel chassis and fasteners
- Encoder gear motors (or motors + separate encoders)
- IMU module (attitude/gyro/accel board; model varies)
- Ultrasonic distance module (optional)
- Battery holder / power wiring (varies by battery type)
- Cables, standoffs, brackets (varies)

### Capabilities (firmware/features) — verify in your firmware/build
Product listings sometimes mention:
- PID balance control
- IMU-based attitude estimation
- Encoder feedback usage
- App/remote control modes
- Ultrasonic obstacle behaviors (avoid/follow)

Treat these as **firmware-dependent** until you confirm them on your build.

## Before power-on: build and safety sanity checks

### Mechanical checks (no firmware needed)
- Wheels spin freely by hand without rubbing the chassis.
- Nothing can touch the wheels when the body tilts (wires, battery holder, sensor bracket).
- Fasteners are tight enough that the IMU and control board cannot rotate relative to the chassis.
- The robot can tip forward/back smoothly; no “sticky” point near the balance position.
- Center of mass is roughly above the wheel axle line (avoid extreme nose-heavy builds).

### Safety setup
- Use a simple “test stand”: hold the robot by the top plate or keep it lightly suspended so wheels can spin during first tests.
- Keep a quick power-disconnect option (unplug battery / switch) in reach.
- Start on a flat surface with space around it; avoid edges and clutter.

## Firmware bring-up checklist (keep it observable)

This section is intentionally generic. The goal is to verify *signs, directions, and signals* before tuning gains.

### 1) Establish a minimal “sensors-only” mode
Confirm you can read, log, or display:
- IMU attitude estimate (at least pitch / tilt)
- Encoder counts or speed estimate for each motor (if your build has encoders)

Acceptance checks:
- When the robot is held still, the reported tilt is stable (small drift is normal; large jumps are not).
- Tilting the robot forward/back changes the reading in a consistent direction (write down your sign convention).

### 2) Verify motor direction and encoder direction (do not skip)
Do these one at a time, low power:
- Command **left motor forward** briefly: does the left wheel rotate “forward” as you define it?
- Check **left encoder** (if present): does its count increase for “forward” rotation?
- Repeat for right motor / right encoder.

If either encoder sign is inverted relative to motor direction, fix it now (software inversion is fine). Balancing is much harder if signs fight each other.

### 3) Add output limits before any balancing attempt
Set conservative limits (conceptually):
- Max motor command (cap PWM/output)
- Rate limiting (optional but helpful)
- A hard “disable motors” state you can enter quickly

## IMU + balance geometry: define your conventions once

Write these down before tuning so your logs are readable:
- **Pitch = 0**: the chassis is upright at your intended balance point.
- **Pitch sign**: which direction is positive (nose forward or nose backward).
- **Motor command sign**: which sign moves the robot forward.
- **Control goal**: drive pitch error toward zero *without* runaway wheel acceleration.

If your “upright” pitch is not exactly zero due to mounting angle, define a **pitch_offset** (calibration) rather than forcing PID to fight a bias.

## First balance attempts (validation-first, no promises)

Start with a controlled, repeatable procedure:
1. Put the robot in a safe test stance (lightly held, or wheels free to spin).
2. Enable balancing for 1–2 seconds only, then disable.
3. Observe: wheel spin direction, response timing, and whether output saturates immediately.
4. If it saturates immediately, stop and fix sign/scale issues before tuning gains.

Red flags that usually mean a sign or unit problem (not “bad PID”):
- Wheels accelerate harder as the robot falls further (wrong sign).
- Tiny tilts cause instant max output (scale too large, missing limits).
- Output is stuck at a constant value even when tilt changes (sensor not updating or control not running).

## PID calibration checklist (practical, incremental)

Tune in stages. Keep changes small and record each change with a brief note.

### Stage A — P-only (prove the loop “pushes back”)
Goal: when the robot tilts, the wheels should try to correct the tilt direction (not amplify it).

Checklist:
- Set I = 0, D = 0.
- Increase P gradually until you see a clear corrective response.
- If it oscillates rapidly or “buzzes,” P is too high *or* your measurement is noisy / delay is high.

### Stage B — Add D (reduce overshoot and wobble)
D helps damp oscillation but is sensitive to noise.

Checklist:
- Keep I = 0.
- Add a small D and increase slowly.
- If D makes the output jittery, consider derivative filtering or reducing sensor noise (implementation depends on your firmware).

### Stage C — Add a little I (handle slow drift / bias)
Only after PD behaves reasonably.

Checklist:
- Add a small I to correct slow leaning or creeping.
- Add anti-windup behavior conceptually (e.g., limit integral term) so the robot doesn’t “charge up” when held or saturated.
- If it slowly builds into a runaway, I is too high or windup isn’t controlled.

### Quick symptom-to-check map (use as notes while tuning)
- **Runs away immediately** → sign convention wrong (pitch or motor direction), or output scaling too aggressive
- **Fast wobble in place** → P too high, D too low, noisy derivative, or too much delay
- **Slow sway / lazy correction** → P too low, output limit too tight, or control rate too low
- **Leans and slowly creeps** → add small I or adjust pitch_offset (mounting/calibration)
- **Stable only when held** → output limits, friction, or center-of-mass may be dominating; revisit mechanics and scaling

## Adding “extras” after balance works (optional, validate on your build)

Some kit listings mention app control and/or an ultrasonic module. Treat both as *inputs* to the balance controller once upright control is reliable.

### App control input (integration guardrails)
- Start with very small command ranges.
- Prefer “target speed” or “target angle offset” style commands rather than directly overriding motor PWM.
- Keep a deadman/timeout: if commands stop, return to neutral.

### Ultrasonic behavior (keep it slow)
- Validate sensor readings first with the robot stationary.
- Use it for gentle forward/back speed bias once balancing is stable.
- Avoid abrupt changes that can kick the robot out of its balance envelope.

## Documentation checklist (WordPress + GitHub-friendly)

- Only label items as “included” if you verified them from your physical kit; otherwise label as “varies by kit/revision.”
- Add a short “Conventions used” block (pitch sign, forward direction) so readers can match logs to behavior.
- Keep PID guidance value-free unless you have verified gains for a specific hardware + firmware revision (and label that scope clearly).
- Link readers to the kit/product pages for ordering context, and to the tutorials hub for other guides:
  - Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
  - Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
  - Tutorials hub: https://feigen8n.online/tutorials/

## Pre-publish verification notes (only include if you can confirm)
- Confirm the exact IMU module and its mounting orientation for the kit revision you are documenting (especially if adding pin maps or screenshots).
- Confirm the firmware structure and build steps for the revision you are referencing before naming directories, file paths, or configuration fields.
- Avoid publishing PID “starter values” unless they are tied to a specific, verified hardware + firmware combination and clearly labeled.
