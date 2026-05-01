# STM32 Self-Balancing Car Kit — Setup & PID Calibration Notes

This repository is a verify-on-your-build guide for bringing up a two-wheel STM32 self-balancing robot car and tuning a balance controller. It uses checklist-style steps so you can confirm signs, wiring, and control-loop behavior on your specific hardware revision without assuming exact board or sensor models.

## What this guide covers
- Safe bring-up sequencing (sensors first, motors later).
- IMU orientation/sign checks before tuning.
- Encoder direction and motor polarity checks.
- A practical PID tuning workflow (P → D → I) with safety limits.
- Keeping optional add-ons isolated until baseline balance is repeatable.

## What to verify on your kit (varies by seller/listing)
Confirm what your unit actually has before wiring or enabling features:
- Controller board type and power input requirements.
- IMU module interface (I2C/SPI) and voltage level.
- Motor driver wiring and motor polarity conventions.
- Encoder channels (A/B), power, and direction convention.
- Optional control method (for example, app/remote control module), if your listing includes it.
- Optional sensors (for example, distance sensors), if your listing includes them.

## Bring-up sequence (recommended)
1) **Mechanical sanity**
- Chassis rigid; wheels spin freely; IMU mounted firmly (minimal wobble).

2) **Power safety**
- Start with wheels off the ground.
- Use a consistent power-off habit: disconnect battery first.

3) **IMU first, motors later**
- Start with motors disabled in firmware (or motor outputs disconnected).
- Read your attitude signal (tilt estimate or raw accel/gyro).
- Tilt forward/backward slowly and confirm the reported sign matches reality.
  - If inverted, fix axis mapping/mounting before continuing.

4) **Encoder direction check**
- Rotate each wheel by hand; confirm counts change smoothly.
- Decide and document a convention (for example: “forward rotation = positive delta” on both sides).

5) **Motor polarity check**
- Command low power briefly per motor and confirm “forward” is consistent.
- If one side is reversed, swap motor leads or invert that channel in firmware.

## Control loop notes (implementation-agnostic)
A balancing robot typically needs:
- A stable tilt estimate from the IMU (fusion method depends on your firmware).
- A fixed-rate control loop with understood sign conventions and saturation behavior.
- Optional encoder feedback to assist with drift/speed damping (exact approach varies).

Do not begin aggressive tuning until loop rate, signs, and output limits are confirmed.

## PID calibration checklist
1) **Start conservative**
- Low gains, low output clamp, and a clear disable condition (for example: cut motors if tilt exceeds a threshold).

2) **P-term first**
- Increase P gradually until it resists falling.
- If it accelerates the fall, stop: a sign convention is wrong.

3) **Add D for damping**
- Increase D slowly to reduce wobble/overshoot.
- If twitchy/noisy, reduce D and/or filter the signal you differentiate.

4) **Add I last (only if needed)**
- Use small I to correct slow bias.
- Add anti-windup (clamp/reset) to prevent long recovery after saturation.

5) **Progress in stages**
- Wheels-in-air → on-ground with support → short free-standing attempts.

## Optional add-ons (only after balance is stable)
- App/remote control (if present): treat as high-level commands (target speed/turn) layered on top of balance.
- Extra sensors (if present): start read-only (telemetry) before enabling behavior changes.

## Related
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Tutorial: `stm32-self-balancing-car-setup`
