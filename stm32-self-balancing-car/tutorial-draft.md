---
status: draft
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: true
publish_target: WordPress
---

# STM32 self-balancing car setup and PID calibration checklist (draft)

## What this draft covers
This tutorial is a practical, step-by-step checklist for getting a two-wheel **STM32 self-balancing car** kit to the point where you can safely tune balance control. You should verify the exact kit contents, wiring, firmware steps, and observed behavior on **your own build** before treating any step as complete.

Related pages for reference:
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/

## Before you start (safety + expectations)
- Work on a clear bench and be ready to cut power quickly during early tests.
- Assume motor direction, IMU orientation, and encoder polarity may be different from what you expect until you confirm them.
- Do not run “balance mode” with the wheels free-spinning at full power for long periods, because it can overheat motors or drivers on some builds.
- Keep the robot lifted (wheels off the table) for the first firmware and sensor checks.

## Confirm what you actually have (parts checklist)
The kit listing describes a balancing chassis with an STM32-based controller plus sensors and modules (for example: an **IMU attitude sensing module**, **encoder gear motors**, and an **ultrasonic module**). Confirm your box matches your order and identify:
- Controller board and its power input range/connector type (from the board marking or seller notes).
- IMU board model and how it connects (I2C/SPI pins and voltage level).
- Left/right motors and the encoder connections (A/B channels and power leads).
- Any optional control method (for example, “app control support” is mentioned on the listing, but you must confirm the specific module and procedure on your unit).

## Mechanical assembly checks (do these before wiring)
- Tighten the chassis hardware and confirm the wheels spin without rubbing.
- Ensure the IMU mounting surface is rigid and not flexing with motor vibration.
- Mount the IMU so its axes are consistent with your firmware’s expectation (forward/back, left/right, up/down). If you do not know the expected orientation, plan to verify it in the sensor test step.

## Wiring checklist (verify with your board labels)
- Power: battery holder/output to the correct power input on the controller or motor driver, and confirm polarity before connecting.
- Motors: left/right motor leads to motor driver outputs, but do not assume direction is correct yet.
- Encoders: connect encoder power/ground and the signal channels to the correct GPIO pins; label A/B so you can swap in software or wiring if needed.
- IMU: connect SDA/SCL (or SPI lines), power, and ground; confirm the IMU voltage matches the controller’s logic level.
- Ultrasonic (if used): connect trig/echo and power/ground, and confirm any echo-level shifting requirements for your board.

## Firmware bring-up (minimum viable checks)
- Flash firmware using your preferred STM32 workflow, and confirm you can rebuild and re-flash repeatedly.
- Enable a “safe mode” or “test mode” if available (motors disabled) so you can validate sensors first.
- Confirm the control loop timing in the firmware is stable (for example, a periodic timer interrupt rather than a variable-delay loop), because unstable timing makes PID tuning unreliable.

## Sensor sanity checks (must pass before PID tuning)
With the robot held still on the bench:
- IMU: read tilt angle (or raw accel/gyro) and confirm the sign makes sense when you gently tip the chassis forward and backward.
- Gyro: confirm the rate sign matches the direction you rotate the chassis.
- Encoders: rotate each wheel by hand and confirm counts change smoothly, and that left/right channels do not appear swapped.
If any sign is inverted, fix it now (swap wires, swap A/B, or invert in software), then repeat the checks.

## PID calibration checklist (balance first, then features)
1. **Start with balance only.** Disable extras like ultrasonic behaviors and remote/app commands until the robot can stand reliably.
2. **Set motor limits early.** Add a conservative output clamp so early tuning cannot drive the motors to extreme values.
3. **Tune P first.** Increase proportional gain gradually until the robot starts to “fight” to stay upright, then back off if it oscillates violently.
4. **Add D to reduce overshoot.** Increase derivative gain to damp fast tipping and reduce wobble, while watching for noise sensitivity from the IMU.
5. **Add a small I only if needed.** Integral helps correct slow bias (uneven motors, slight center-of-mass offset), but too much I can cause slow drift and sudden runaway after saturation.
6. **Check direction again.** If it instantly accelerates and falls harder, the feedback sign is likely wrong (angle sign, motor direction, or mixing).
7. **Validate on the floor.** After stable bench tests, test short balance attempts on a flat surface, with your hand ready to catch it and cut power.

## Troubleshooting (fast symptoms → likely cause)
- Immediate full-speed runaway: feedback sign wrong, motor direction wrong, or angle reference wrong.
- High-frequency shaking: P too high, D too high with noisy gyro, or loose IMU mounting.
- Slow drifting then sudden lurch: integral windup or output saturation without anti-windup handling.
- Balance works when lifted but fails on the floor: insufficient torque, wrong center of mass, or encoder/velocity terms misconfigured.

## Next steps
Once upright balance is repeatable, re-enable optional features one at a time (encoder speed control, app control, ultrasonic behaviors) and re-check stability after each change. For shopping or kit reference details, use the kit/product pages linked at the top, and cross-check any claims against your actual hardware before you document them.
