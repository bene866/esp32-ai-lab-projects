# STM32 Self-Balancing Car — Setup & PID Calibration Checklist (Build-Specific)

This repository is a practical bring-up and tuning checklist for a **two-wheel STM32 self-balancing car** build. It prioritizes **observable verification** (what you can measure or see) over assumptions about exact board revisions, IMU models, motor drivers, wiring colors, or firmware forks.

If your kit revision differs from someone else’s, that is normal. Treat every step as **“passed” only after you confirm it on your own hardware**.

## Project purpose

A balancing robot is a closed-loop control system that depends on consistent sensor orientation, correct motor direction, reliable encoder feedback, and sane timing. This README provides a repeatable flow to:

- Confirm IMU readings are plausible and mapped to the expected axes.
- Confirm both motors spin the correct way and respond symmetrically.
- Confirm encoder counts change in the correct direction for each wheel.
- Reach a safe “upright but supported” balance test point.
- Tune PID gains methodically without chasing noise or wiring mistakes.

## Validation status (read before building)

- This repository draft is **documentation-first** and uses **verify-on-your-build** language.
- It does **not** claim your specific kit or firmware is already tested, calibrated, or safe out of the box.
- Only mark steps complete after you validate them with your own measurements (serial logs, scope, multimeter, or on-device telemetry).

## What this repo is (and isn’t)

- It **is** a setup and calibration checklist that matches the typical feature set of this kit category: **PID control, IMU attitude sensing, and encoder motor feedback**.
- It **is not** a guarantee of exact pin maps, exact IMU register settings, or exact motor driver wiring for your seller’s revision.
- It **does not** include secrets, credentials, or vendor-specific private files.

## Safety notes

- During first power-on, keep wheels off the table (use a stand) or remove tires until motor direction and encoder polarity are confirmed.
- Use a current-limited supply if available, or add an inline fuse for early bring-up.
- Do not attempt hands-free balancing until IMU orientation, motor direction, and encoder direction are all confirmed correct.

## Repository structure (adjust to match your actual files)

Use this section as a reference layout. If a folder does not exist in your local checkout, treat it as a placeholder to organize your own work.

- `firmware/` — STM32 project (STM32CubeIDE or equivalent) and configuration.
- `docs/`
  - `docs/checklists/` — printable checklists and tuning logs.
  - `docs/wiring/` — wiring notes and “as-built” photos per kit revision.
  - `docs/media/` — demo videos, serial logs, screenshots (placeholders below).
- `hardware/` — BOM notes, mechanical notes, motor/encoder labeling.
- `tools/` — scripts for log parsing or plotting (optional).
- `README.md` — this guide.

## Prerequisites

- A PC environment capable of building and flashing STM32 firmware (commonly via STM32CubeIDE).
- A way to read basic telemetry (serial console, on-screen debug, or app output if your firmware supports it).
- Basic measurement tools (at minimum a multimeter; a scope helps but is not required).

## Setup notes (before you flash anything)

1. **Identify your exact kit revision.** Record board silkscreen, IMU module marking, motor model, and battery type in a short build log.
2. **Label left vs right.** Mark the chassis left/right and wheel left/right so direction tests are unambiguous.
3. **Mount the IMU consistently.** If the IMU is rotated 90° or upside down relative to the firmware’s expectation, balancing will fail even if the code “runs.”
4. **Check mechanical friction.** Verify both wheels spin freely by hand and the gearbox resistance feels similar on both sides.
5. **Confirm power domains.** Verify which rail powers motors and which rail powers logic, and confirm grounds are shared.

## Wiring & firmware verification checklist (bring-up sequence)

### A) Power and basic boot
- [ ] With motors disconnected (or motor enable disabled), power the board and confirm it boots reliably.
- [ ] Confirm you can flash firmware repeatedly without needing to power-cycle unpredictably.
- [ ] Confirm no component overheats during idle (regulator, driver, MCU area).

### B) IMU sanity (orientation and noise)
- [ ] Log raw accelerometer and gyro values at rest for 10–20 seconds.
- [ ] Confirm gravity appears on one axis near a constant magnitude while the device is stationary.
- [ ] Slowly tilt the chassis forward/backward and confirm the expected axis changes smoothly.
- [ ] Rotate the chassis around yaw and confirm the gyro axis for yaw responds with the correct sign.
- [ ] If you compute pitch/roll, confirm pitch increases in the direction your control code defines as “forward.”

If any axis behaves inverted or swapped, fix mapping/orientation before touching PID gains.

### C) Motor direction (sign correctness)
- [ ] Command a low PWM output (or low speed command) and verify **both wheels spin the intended direction** for “forward.”
- [ ] If one wheel spins opposite, correct it in wiring or in software direction inversion, then re-test.
- [ ] Command “left turn” and confirm the differential motion matches your coordinate system (do not assume).
- [ ] Verify the motor driver enable/standby pins behave as expected (no random movement at boot).

### D) Encoder direction and scale
- [ ] With the robot lifted, spin the left wheel forward by hand and confirm left encoder counts change with a consistent sign.
- [ ] Repeat for the right wheel and confirm the same “forward” definition produces the same sign convention.
- [ ] Confirm both encoders report similar counts per second at the same commanded speed (within reasonable tolerance).
- [ ] If one encoder is reversed, fix A/B channel order (or invert in software) and re-check.

### E) Control loop timing (stability prerequisite)
- [ ] Confirm the control loop update period is stable (no large jitter visible in logs).
- [ ] Confirm IMU sampling and control updates are synchronized or at least consistent.
- [ ] Confirm your filter choice (if any) does not add excessive lag; lag can look like “bad PID” but is a timing issue.

### F) First balance test (supported, not hands-free)
- [ ] Place the robot on a stand so wheels can spin freely, and hold the body near upright.
- [ ] Enable balance control at a conservative output limit.
- [ ] Confirm the wheels respond in the **correct corrective direction** when you gently tip forward/back.
- [ ] If it “runs away” in the wrong direction, stop and fix sign conventions (IMU angle sign and motor sign).

## PID tuning checklist (methodical approach)

Use a written tuning log. Change one variable at a time and record the result.

1. **Start with limits.** Set conservative output clamps and a safe angle threshold that disables motors if the tilt is too large.
2. **P-only stabilization.** Increase `Kp` until the robot begins to resist tilt but does not oscillate violently. If it oscillates immediately, your sign or timing is likely wrong.
3. **Add D to reduce overshoot.** Increase `Kd` gradually to damp oscillation and reduce “bouncing” around upright.
4. **Add I last (if needed).** Introduce `Ki` slowly to reduce steady-state drift. Too much integral causes slow runaway or delayed overshoot.
5. **Check symmetry.** If it behaves differently tipping forward vs backward, check IMU calibration, mechanical balance, and motor matching before forcing PID to compensate.
6. **Verify with encoders.** If your controller uses speed or position feedback, confirm encoder signs and scaling again after each major change.
7. **Confirm real-ground behavior.** After stand testing, test on the ground with a spotter hand nearby and a strict cutoff threshold.

## Troubleshooting (common failure signatures)

- **Instant full-speed runaway on enable:** motor sign inverted, angle sign inverted, or pitch axis mapped incorrectly.
- **Shakes rapidly at small angles:** loop timing too fast/unstable, `Kp` too high, `Kd` too low, or IMU data too noisy.
- **Slow “wobble” that grows:** `Ki` too high, integral windup, or too much filter lag.
- **Balances on stand but fails on ground:** encoder feedback sign/scale wrong, friction mismatch, battery sag under load, or output limits too tight.
- **One wheel does most of the work:** motor wiring mismatch, encoder missing on one side, mechanical drag, or inconsistent PWM channel configuration.

## Demo media placeholders (add your verified artifacts)

Add your own build-specific files under `docs/media/` and reference them here.

- `docs/media/imu-axis-check.mp4` — short clip showing tilt and telemetry response.
- `docs/media/motor-direction-test.mp4` — forward/reverse/turn command demonstration.
- `docs/media/encoder-sign-test.mp4` — wheel spin by hand with live count display.
- `docs/media/first-supported-balance.mp4` — supported upright test (not hands-free).
- `docs/media/tuning-log-YYYY-MM-DD.md` — tuning notes with `Kp/Ki/Kd`, limits, and outcomes.

## Official references

- STM32Cube documentation (STM32CubeIDE): https://www.st.com/en/development-tools/stm32cubeide.html  
- ST motor control resources: https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html  

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/  
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/  
- Tutorial (checklist): https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/  
- Tutorials hub: https://feigen8n.online/tutorials/
