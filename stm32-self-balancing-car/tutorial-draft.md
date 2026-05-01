---
status: draft
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: true
publish_target: WordPress
---

# STM32 Self-Balancing Car Kit: setup + PID calibration checklist (draft)

This is a **review-required** checklist-style tutorial for bringing a **two-wheel STM32 self-balancing car** from “assembled” to “ready to tune.” It focuses on the practical order of operations for **IMU orientation**, **encoder direction**, **motor polarity**, and **PID tuning workflow**—without assuming any specific firmware, pinout, or “known-good” gain values.

The kit/product pages describe this project as a hands-on STM32 balancing robot learning platform with **PID control**, **IMU attitude sensing**, and **encoder motor feedback**, plus **app control support** and an **ultrasonic obstacle module** option. The page also lists the following as included: **two-wheel chassis**, **IMU module**, **encoder gear motors**, **ultrasonic module**, and **battery holder and wiring** (plus “source code and learning materials”).  
(Use this draft as a calibration SOP; only add wiring diagrams, code paths, and parameter screenshots after you verify them.)

## What you should verify *before* powering up
- [ ] **Fasteners & alignment:** wheel hubs tight, chassis not twisted, wheels spin freely without rubbing.
- [ ] **IMU mounting is rigid:** no foam wobble; the IMU board shouldn’t flex when you press it lightly.
- [ ] **Center of mass is reasonable:** battery mounted securely; cables don’t pull the body forward/back.
- [ ] **Wheels can lift safely:** prepare a stand so you can run motors with wheels off the table.

## Minimum “bring-up” checklist (no tuning yet)
### 1) IMU orientation sanity (critical)
You need two things to be true before any PID tuning is meaningful:
- The firmware’s **pitch/tilt sign** matches reality (lean forward → measured pitch changes in the expected direction).
- The IMU’s axes mapping is consistent (you’re tuning the balancing axis, not roll/yaw by mistake).

Checklist:
- [ ] With motors disabled, read a **tilt angle** output (or raw accel/gyro values if that’s all you have).
- [ ] Slowly tilt the robot forward/back by hand and confirm the reported sign/direction is consistent.
- [ ] If direction is inverted, fix it at the source (axis mapping / sign flip), not by “negative PID gains.”

### 2) Encoder direction sanity (critical)
Encoders must agree with motor direction, or your speed/position loops will fight you.

Checklist:
- [ ] Spin the **left wheel forward by hand**; verify encoder count changes smoothly (no random jumps).
- [ ] Spin the **right wheel forward by hand**; verify the same.
- [ ] Confirm **forward motion** corresponds to the same sign for both wheels (or intentionally mirrored if your firmware expects that—document it).

### 3) Motor direction + “failsafe posture”
Before tuning, decide what “corrective action” means:
- If the robot **leans forward**, the wheels should drive **forward** to catch it (common for inverted pendulum setups).  
If your firmware uses the opposite convention, write it down explicitly and keep it consistent across IMU sign + motor sign.

Checklist:
- [ ] With wheels off the ground, apply a small manual tilt and confirm the control output would command the expected direction (even if gains are near zero).
- [ ] Add a **tilt cutoff** (or confirm one exists): beyond a large angle, motors should stop rather than accelerate.

## Calibration: make sensors “boring”
The goal is stable, low-noise signals so your gains don’t compensate for junk.

### IMU offset / bias notes (generic, reviewable)
Without claiming a specific IMU model or library, a typical calibration pass aims to reduce:
- **gyro bias drift** (robot slowly “leans” in software while sitting still)
- **accelerometer offset** (static tilt isn’t close to zero when upright)

Checklist:
- [ ] Place robot in a known **upright reference** (use a small square or visual alignment).
- [ ] Record the reported angle (or accel vector) for ~10–20 seconds.
- [ ] If you see slow drift while perfectly still, investigate gyro bias compensation / filtering.
- [ ] Keep filtering conservative at first: too much filtering can add delay and worsen balance.

### Encoder cleanliness
Checklist:
- [ ] Check for **dropouts** when spinning slowly (counts should not freeze intermittently).
- [ ] Check for **direction flips** near stop (often wiring/noise or debounce issues).
- [ ] If PWM causes encoder noise spikes, add grounding/cable management before touching gains.

## PID tuning order (recommended)
Balancing robots commonly behave best with a staged approach:
1) **Angle/tilt loop** (inner loop): make it “want to stand up.”
2) **Speed loop** (outer loop): stop it from drifting away while balancing.
3) **Turn/yaw loop** (optional): controlled steering once balance is stable.

You can follow this order even if your firmware names loops differently.

## Step 1 — Tune the angle (tilt) loop first
### Start conditions
- [ ] Wheels can spin freely (robot on a stand).
- [ ] Limit output (cap PWM/duty) so mistakes don’t slam the motors.
- [ ] Disable speed/turn control (or set their gains to zero) during initial angle tuning.

### A practical, safe tuning sequence
- **P (proportional):** Increase gradually until the robot starts to “fight” being tilted and returns toward upright.
- **D (derivative):** Add D to reduce overshoot and calm fast oscillations.
- **I (integral):** Leave I off initially; add later only if you see a consistent steady-state lean that P/D cannot remove.

Checklist:
- [ ] With a small forward tilt, the correction is immediate but not violent.
- [ ] If it oscillates rapidly: lower P or increase D slightly.
- [ ] If it returns slowly and feels “lazy”: increase P slightly.
- [ ] If you hear harsh buzzing at rest: D may be amplifying noise; reduce D or improve filtering.

## Step 2 — Add the speed loop to prevent runaway drift
Once the tilt loop can stabilize on a stand (and briefly on the ground with a hand ready to catch it), the next problem is usually **creeping**: it balances but slowly rolls away.

Conceptually, the speed loop should output a small **tilt bias** to cancel drift.

Checklist:
- [ ] Enable speed feedback from encoders (confirm sign is correct).
- [ ] Start with a small speed P (or equivalent) so it gently counters drift.
- [ ] Add speed I only if it keeps drifting steadily in one direction.
- [ ] Implement anti-windup (or keep I small): if it falls over, the integrator should not “store” huge commands.

## Step 3 — Turning control (only after stable balance)
Turning is easiest when it is layered as a differential command between wheels.

Checklist:
- [ ] Confirm left/right motor outputs are symmetric at neutral.
- [ ] Add a small turn command and verify it doesn’t destabilize tilt.
- [ ] Rate-limit turn commands (especially if using “app control support”) so a sudden joystick snap doesn’t cause a fall.

## Optional module: ultrasonic obstacle behavior (keep it simple)
The kit pages mention an ultrasonic module and obstacle behaviors. Treat this as an add-on once balancing is reliable.

Safe integration pattern:
- Use ultrasonic only to generate a **slow speed target** (e.g., “approach/avoid”), not to directly modulate the angle loop.
- Filter distance readings and clamp the speed target so it cannot request abrupt accelerations.

Checklist:
- [ ] If distance reading is invalid/noisy, default to “no action” rather than sudden reverse.
- [ ] Keep obstacle behavior disabled during PID tuning sessions.

## Quick symptom-to-fix map (field notes)
- **Immediate violent flip on enable:** IMU axis/sign wrong, motor direction wrong, or output not limited.
- **Fast jitter/buzzing while upright:** too much D, noisy IMU, or too high control frequency without filtering.
- **Slow wandering while “balanced”:** encoder sign/scale issue, speed loop not enabled/tuned, or integrator too weak/too strong.
- **Balances only when held, fails on ground:** friction differences, wheel alignment, motor deadband, or insufficient torque at low PWM.

## Related pages (for readers who want the kit context)
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/

## Review checklist for publishing this draft
- [ ] Add confirmed firmware parameter names (exact UI labels) only after verification.
- [ ] Add real photos/screenshots only after you confirm filenames and rights.
- [ ] Add wiring/pinout only if you can cite the board silkscreen or an official diagram from the repo/materials.
- [ ] Keep any “included items” list aligned with the kit page wording (don’t invent parts).
