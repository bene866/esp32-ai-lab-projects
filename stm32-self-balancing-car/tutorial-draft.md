---
status: draft
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: true
publish_target: WordPress
---

# STM32 self-balancing car setup and PID calibration checklist

This is a practical, review-first checklist for bringing up a two-wheel STM32 self-balancing robot car kit that focuses on PID control, IMU attitude sensing, and encoder motor feedback. It avoids assuming specific wiring, firmware, or measured performance unless you confirm them on your bench.

Related pages:
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- More guides: https://feigen8n.online/tutorials/

## What this kit is (from the kit page text)

The kit is presented as a hands-on STM32 self-balancing robot car for learning:
- PID control
- IMU attitude sensing
- Encoder motor feedback
- App control support
- Optional ultrasonic obstacle avoidance / following

The kit page also lists “source code and learning materials” and a set of included modules/parts; treat that list as what’s *advertised*, and verify what you received before planning your build.

## Before you power anything (10-minute safety pass)

- Confirm the chassis is mechanically free: wheels spin without rubbing, nothing binds, fasteners are tight.
- Keep wheels off the desk for first power-up (stand, block, or hold the chassis) so a wrong motor direction doesn’t launch the robot.
- Start with a current-limited supply if you have one; otherwise, be ready to cut power quickly.
- Do not connect/disconnect motors or modules while powered.

## Inventory and “known/unknown” log

Create a short bench log (a single note is fine) with:
- Battery type you plan to use (do not assume voltage or connector type).
- IMU module marking/model (write what’s printed on the board).
- Motor/encoder connector labeling (photos help).
- Any ultrasonic module and any app-control module (if present on your kit).

If something on the kit page list is missing (or you have extras), note it now—PID tuning will be confusing if the sensor stack isn’t what you think it is.

## Power + orientation checklist (no tuning yet)

### 1) IMU orientation sanity check
You must confirm these before any balancing attempt:
- The “forward” direction of the robot (pick a reference: the side you want to be the front).
- The IMU board’s orientation relative to the chassis (which way is up/forward).
- The sign convention your firmware uses for “tilt forward” vs “tilt backward”.

If you don’t have a live angle readout, add one before attempting balance (even a serial print is enough). Do not tune PID blindly.

### 2) Motor direction sanity check
With the robot held safely:
- Apply a small manual command (or whatever minimal motion test your firmware provides).
- Confirm “forward command” makes both wheels drive forward.
- If one side is reversed, fix motor wiring or the motor direction setting *before* touching PID.

### 3) Encoder feedback sanity check
Encoders are only useful if they count correctly:
- Spin each wheel by hand and confirm the corresponding encoder count changes.
- Confirm left wheel affects “left” count, right wheel affects “right” count.
- Confirm count direction (increasing vs decreasing) matches your motion convention.

If encoder direction is inverted, speed/position loops can fight the balance loop.

## Sensor calibration checklist (keep it explicit)

Because the exact IMU module and firmware are not specified here, treat calibration as a checklist of observable outcomes:

- Gyro bias: after the robot sits still for ~10–20 seconds, the reported angular rate should be near zero and not drifting rapidly.
- Accelerometer bias: when the robot is upright and stationary, the computed tilt angle should be stable (small noise is normal; large slow drift is not).
- Vibration: if motor vibration makes the angle estimate noisy, improve mechanical mounting and cable routing before increasing control gains.

Record: “angle noise at rest” and “angle noise with motors spinning in air”.

## Control stack: confirm your loop structure (don’t assume)

Many self-balancing robots use:
- An inner **balance loop** (tilt angle/tilt rate -> motor command)
- Optional **speed loop** using encoders (to prevent drift)
- Optional **steering/turn loop** (differential motor command)
- Optional ultrasonic behaviors (avoid/follow)

Before tuning, write down what you actually have:
- What is the balance loop input? (angle only, angle + rate, etc.)
- Are encoders used in the balance loop, the speed loop, or both?
- Is there an integral term in the balance loop, the speed loop, or both?

If you can’t answer these, pause and inspect your firmware documentation/materials (the kit page claims learning materials exist, but their exact contents are not verified in this draft).

## PID tuning workflow (checklist style)

### Step 0: choose a controlled test condition
Pick one:
- “Wheels in the air” test for direction/sign and oscillation detection.
- “Lightly supported on the ground” (hands-on support) for first balance attempts.

Do not start with free-standing balance attempts.

### Step 1: get the sign right (the “push-back” test)
With very low gains:
- Tilt the robot forward slightly by hand.
- The controller should command wheels to drive forward (to push back under the center of mass), not accelerate the fall.

If it drives the wrong way, fix sign conventions (angle sign, motor sign, or mixing) before continuing.

### Step 2: tune proportional (P) for “stiffness”
- Increase **Kp** gradually until the robot reacts quickly but starts to oscillate.
- Back off slightly from the first sustained oscillation.

Record:
- Kp where oscillation begins
- Kp you settle on initially

### Step 3: add derivative (D) for damping
- Increase **Kd** gradually to reduce oscillation and overshoot.
- Watch for high-frequency jitter; if it appears, you may be amplifying sensor noise.

If D causes jitter:
- Reduce Kd, and/or improve filtering, and/or reduce mechanical vibration.

### Step 4: add integral (I) only if you need it
Integral can help with slow bias (e.g., slight CG offset), but it can also make recovery worse.
- Start **Ki** extremely small.
- Add only enough to reduce steady drift without causing slow “wind-up” and delayed tipping.

Anti-windup is strongly recommended if your firmware supports it; if it doesn’t, keep Ki conservative.

### Step 5: introduce encoder speed loop (if present)
Only after balance is stable:
- Enable or tune the speed loop to reduce drifting across the floor.
- Keep speed-loop gains modest so it doesn’t fight the balance loop.

A common failure mode: speed loop too aggressive → robot “hunts” forward/backward even when upright.

### Step 6: steering + app control (if present)
Once balance + speed are stable:
- Add steering commands slowly.
- Confirm turning doesn’t collapse the balance loop (turning changes load and can excite oscillations).

### Step 7: ultrasonic behaviors (if present)
Obstacle avoidance/following can inject sudden speed targets:
- Rate-limit speed target changes.
- Prefer smooth ramps over step changes.

## “Looks stable” acceptance checklist (what to verify)

Without claiming measured performance, here are practical pass/fail checks you can run:

- Upright hold: can remain upright when lightly perturbed (tap test) while supported.
- Recovery: can recover from a small tilt without escalating oscillation.
- Noise: motors do not buzz violently at rest (buzzing often means too much D/noise).
- Drift: does not continuously walk away due to bias (address with calibration, small I, or speed loop).

Write down what failed and under what conditions; it makes iteration faster than guessing.

## Troubleshooting map (symptom → likely causes)

- **Immediately accelerates into a fall**
  - Motor direction inverted, angle sign inverted, or mixing wrong.

- **Slow wobble that grows over seconds**
  - Too much I, or gyro bias/drift not handled, or speed loop fighting balance.

- **High-frequency shiver/buzz**
  - Too much D, noisy IMU signal, poor filtering, mechanical vibration.

- **Balances in the air but fails on the ground**
  - Ground friction/load changes, insufficient torque, battery sag, encoder loop interaction.

- **Turns cause sudden collapse**
  - Steering mixing too strong, asymmetric motors, or speed/turn loop too aggressive.

## Notes for reviewers (what to verify before publishing)

- Confirm which STM32 board/MCU is actually used in this kit (not specified in the audit excerpt).
- Confirm the exact IMU module model(s) shipped.
- Confirm what “app control support” means in this kit (BLE? other?) and what is included.
- If you want this tutorial to link to firmware paths in the GitHub repo, only add those links after verifying the files exist in `stm32-self-balancing-car` and match the described control structure.
