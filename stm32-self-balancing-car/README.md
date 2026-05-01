# STM32 Self-Balancing Car Kit — Setup & PID Calibration Notes (Draft)

This repository is a technical, verify-on-your-build guide for a **STM32-based two-wheel self-balancing robot car** that uses **IMU attitude sensing** plus **encoder motor feedback** for closed-loop control. It is written to support careful bring-up, repeatable checks, and PID tuning without assuming any exact board or sensor part number beyond what your kit includes.

## What this project covers

- Establish a safe bring-up sequence for a balancing robot.
- Confirm IMU orientation and basic angle stability before driving motors.
- Verify encoder direction and motor polarity so “forward” is consistent.
- Tune a practical PID loop with incremental, observable changes.
- Keep optional modules (app control, ultrasonic) from interfering with core balance control until the robot can stand reliably.

## Hardware included (kit-level overview)

From the kit description, you should have:
- STM32-based self-balancing robot car kit (controller + chassis)
- Two-wheel balancing chassis
- IMU attitude sensing module
- Encoder gear motors
- Ultrasonic module
- Battery holder and wiring
- Source code and learning materials (exact contents may vary)

## Validation status (as of 2026-04-30)

- This README is a **draft intended for human review**.
- All procedures are **checklists**; they must be validated on your specific build.
- No hardware behavior (balance, speed, app function, ultrasonic avoidance) is claimed as verified here.

## Bring-up sequence (recommended)

1) **Mechanical sanity**
- Confirm the chassis is rigid and both wheels spin freely.
- Ensure the IMU module is firmly mounted and does not wobble.
- Keep wiring strain-relieved so cables do not tug on the IMU or motors.

2) **Power safety**
- Start with the robot **lifted off the table** so wheels can spin without launching.
- Use a clear “power off” habit: unplug battery first, then handle wiring.

3) **IMU first, motors later**
- Power the controller with motors disabled in firmware (or motor driver outputs disconnected).
- Read and display the attitude-related outputs you rely on (for example: tilt angle estimate).
- Slowly tilt the chassis forward/backward by hand and confirm the reported sign matches reality.
  - If the sign is inverted, fix the axis mapping or mounting orientation before continuing.

4) **Encoder direction check**
- With wheels off the ground, command a low duty/low speed test for each motor independently.
- Spin a wheel by hand and confirm the encoder count changes smoothly and consistently.
- Decide and document your convention:
  - “Forward wheel rotation” must produce a positive encoder delta for both sides (or a clearly documented alternative).

5) **Motor polarity check**
- If one motor spins opposite your “forward” command, resolve it by swapping motor leads or by inverting that motor channel in firmware.
- Do not begin PID tuning until “forward” is consistent across both motors.

## Control loop notes (practical, not part-specific)

A balancing robot usually needs:
- A stable **tilt estimate** from the IMU (sensor fusion approach depends on your code/materials).
- A fast control loop that outputs motor effort to reduce tilt error.
- Encoder feedback to help with speed/position damping or drift control (implementation varies).

Treat “upright” as a measurable setpoint (often near zero tilt, after calibration), and ensure your loop rate, sign conventions, and saturations are understood before tuning gains.

## PID calibration checklist (incremental)

Use small steps and log what changes.

1) **Start conservative**
- Use low output limits and low gains so the robot cannot violently accelerate.
- Add a dead-man condition if available (for example: disable motors when tilt exceeds a threshold).

2) **P-term first**
- Increase proportional gain until the robot begins to “fight” falling, then back off slightly if it oscillates.
- If it accelerates the fall instead of correcting it, your sign convention is wrong (do not continue).

3) **Add D for damping**
- Increase derivative gain gradually to reduce oscillation and overshoot.
- If the output becomes noisy or twitchy, reduce D or filter the tilt estimate more aggressively.

4) **Add I last (only if needed)**
- Introduce integral gain slowly to correct steady bias (for example: slight lean needed to hold).
- Use anti-windup (clamps or reset) to avoid long recovery after saturation.

5) **Retest with realistic constraints**
- Move from “wheels in air” to “on ground with a support” to “free-standing” only when each stage is stable.
- Keep optional features (app control, ultrasonic behaviors) disabled until balance is repeatable.

## Optional modules: keep them isolated early

- **App control support**: treat as a high-level input (target speed/turn rate) layered on top of a stable balance controller.
- **Ultrasonic module**: start as read-only telemetry; enable avoidance/following logic only after baseline balance is proven.

## Demo media placeholders (add your files)

Place build evidence and short clips under a folder you choose (example below). Use filenames that clearly match what they show.

- `docs/media/bench-photo.jpg` — kit assembled on bench (static)
- `docs/media/imu-mount-closeup.jpg` — IMU mounting orientation
- `docs/media/wheels-off-ground-test.mp4` — first motor + encoder checks
- `docs/media/first-balance-attempt.mp4` — first supported balance attempts
- `docs/media/pid-tuning-notes.md` — dated tuning log with gain changes and observations

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial slug: `stm32-self-balancing-car-setup`
