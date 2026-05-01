# STM32 Self-Balancing Car — Setup & PID Calibration Checklist (Verify on Your Build)

This repository is a **technical, checklist-style bring-up guide** for a **two-wheel STM32 self-balancing robot car** that uses **PID control**, **IMU attitude sensing**, and **encoder motor feedback**. It is written to be useful even when your kit revision, PCB layout, IMU module, motor driver, or firmware baseline differs from someone else’s.

Primary use cases:
- **STM32 self balancing car kit** bring-up from “assembled” to “controllable”
- **IMU robot car setup** validation (raw sensor sanity → stable angle estimate)
- **Self balancing robot PID tuning** workflow (balance first, then motion)

---

## Project Purpose

A self-balancing robot usually fails for a small number of reasons: wrong IMU axis/sign, wrong motor direction, noisy encoder wiring, bad power integrity, or an unstable PID (often all of the above). The purpose of this README is to provide a **repeatable pass/fail sequence** so you can:
1) confirm sensing is credible,  
2) confirm actuation is correct,  
3) only then close the loop and tune PID safely.

This is **not** a promise of a universal firmware image. Treat every step as “passed” only after you confirm it on your own hardware.

---

## Validation Status (Scope)

- **Status:** Documentation-first checklist draft intended for **hardware-specific verification**.
- **What is validated here:** The workflow, ordering of checks, and common failure patterns.
- **What is not claimed:** No claims are made that any specific board/IMU/motor driver, pin map, or closed-loop behavior is correct on your kit without your confirmation. No unverified hardware tests are claimed.

---

## What You Need (Minimum)

Hardware (varies by revision; verify your kit contents):
- STM32-based controller board (kit-specific)
- 2-wheel chassis with **encoder motors**
- IMU module (kit-specific)
- Motor driver stage (kit-specific)
- Battery + power switch/wiring appropriate for your kit

Tools:
- A development environment that can build/flash STM32 firmware (commonly STM32CubeIDE; see references below)
- A stable bench setup to keep the robot from launching off the table during first tests

---

## Repository Structure (Recommended)

This repository may not match your exact firmware layout. Use the structure below as a practical way to keep bring-up artifacts organized, and adjust to your tree.

- `README.md` — this checklist and troubleshooting
- `docs/` — deeper notes (sensor axes, pin maps, tuning logs, screenshots)
- `firmware/` — STM32 project workspace (if you keep source here)
- `tools/` — small scripts/utilities used during bring-up (optional)
- `media/` — demo videos and photos referenced by the README
- `hardware/` — wiring diagrams, connector photos, BOM notes (optional)

If your repository already has a different layout, keep the intent: **separate firmware, documentation, and media** so each can be reviewed and updated independently.

---

## Setup Notes (Before You Flash Anything)

1) **Make the bench safe**
   - Lift the wheels off the bench or use a stand so the chassis can’t drive away.
   - Have a quick way to cut power. Expect sudden full-speed motor output during early tests.

2) **Start with observability**
   - Ensure you can print or log: IMU raw values, computed angle, encoder counts, and motor command output (PWM or equivalent).
   - If your firmware has a debug console or telemetry, use it. If it does not, add minimal logging before tuning.

3) **Keep defaults conservative**
   - Use modest motor command limits for early tests.
   - Avoid integral action until your signs, axes, and loop timing are confirmed.

---

## Wiring & Firmware Verification Checklist (Pass/Fail)

### A) Mechanical Preflight
- [ ] Wheels spin freely by hand (no binding, no rubbing)
- [ ] Chassis is symmetric enough that it can stand near upright without twisting
- [ ] IMU module is rigidly mounted (no foam wobble, no loose screws)
- [ ] Encoder disks/magnets are aligned and not scraping

### B) Power & Polarity (Do This First)
- [ ] Battery polarity confirmed end-to-end (battery → switch → board → motor driver)
- [ ] Ground is common between controller, motor driver, and sensors
- [ ] Power wiring is secure (no intermittent contact when you move the chassis)
- [ ] First power-on is done with the robot restrained and wheels unloaded

### C) Motor Direction (Open-Loop Only)
Goal: when you command “forward,” both wheels spin in a physically forward direction.
- [ ] Command low duty cycle to left motor only; verify direction
- [ ] Command low duty cycle to right motor only; verify direction
- [ ] If reversed, fix in **software sign** or **wiring** (choose one method and document it)
- [ ] Confirm both motors stop cleanly at zero command (no creeping)

### D) Encoder Sanity
Goal: encoder counts change smoothly and the sign matches wheel direction.
- [ ] With the wheel spun by hand, encoder counts update without dropouts
- [ ] Left encoder increases for forward rotation (define and keep consistent)
- [ ] Right encoder increases for forward rotation (same convention)
- [ ] No obvious noise when the wheel is stationary (counts should not chatter)

### E) IMU Raw Sanity (Before Any Filtering)
Goal: raw accelerometer/gyro signals respond plausibly.
- [ ] With the robot stationary, gyro readings are near zero (bias is OK; drifting wildly is not)
- [ ] Tilting the chassis changes accelerometer axes in the expected direction
- [ ] Rotating the chassis by hand changes gyro axes in the expected direction
- [ ] IMU axes and sign are written down (this avoids endless “it oscillates” tuning loops)

### F) Angle Estimate Sanity (Filter/Complementary/Kalman—Whatever You Use)
Goal: the computed angle is stable, low-noise, and correct in sign.
- [ ] When the chassis tips forward, the computed pitch angle changes in the correct direction
- [ ] When returned to upright, the angle returns near zero (or your defined reference)
- [ ] Noise level is acceptable (if not, fix mounting, wiring, or filtering before PID)

### G) Control Loop Timing
Goal: your control update rate is stable and known.
- [ ] Log/measure the loop period (target depends on your design; consistency matters more than a specific number)
- [ ] Verify sensor read + compute + motor update fits inside the loop budget
- [ ] If the loop jitter is large, fix scheduling/interrupt priorities before tuning

---

## PID Tuning Checklist (Balance First, Then Motion)

### 1) Balance Loop Only (No Speed/Position Targets)
- [ ] Start with **P only** on angle: raise P until the robot *tries* to correct, then back off if it becomes aggressive
- [ ] Add **D** to reduce overshoot/oscillation; increase D until it damps, not until it buzzes
- [ ] Add **I** last and sparingly; I is for steady bias (slight lean, motor mismatch), not for making an unstable loop “work”

Practical rules (verify on your build):
- If it **falls without fighting**, your sign/axis is likely wrong or P is far too low.
- If it **snaps violently** and amplifies the fall, motor direction or angle sign is likely reversed.
- If it **high-frequency chatters**, D may be too high, angle is too noisy, or loop timing is inconsistent.

### 2) Add Speed / Drift Control (After Upright Balance Works)
- [ ] Confirm encoders are clean and signed correctly before enabling speed control
- [ ] Start with a small proportional correction based on wheel speed/position to reduce drift
- [ ] Increase slowly; speed control that is too strong can destabilize balance

### 3) App Control / Commands (Last)
If your build supports app control (kit-dependent), treat it as a command source layered above stable balance:
- [ ] Verify command mapping (forward/back/turn) at low limits
- [ ] Ensure command loss or disconnect returns to a safe state (stop/neutral)

---

## Troubleshooting (Symptoms → Likely Causes)

- **Instant full-power flip on enable**
  - Wrong motor direction, wrong angle sign, or control output saturation too high

- **Slow lean then runaway drive**
  - Missing/weak integral bias correction, encoder sign mismatch, or angle zero reference offset

- **Oscillates at low frequency (rocking)**
  - P too high, D too low, or loop delay too large

- **Buzzing / jitter at high frequency**
  - Noisy angle estimate, D too high, encoder noise coupling into control, or power integrity problems

- **Encoders “random walk” when stopped**
  - Wiring noise, poor grounding, or incorrect pullups/levels (kit-specific—verify your electronics)

- **Angle estimate drifts or jumps**
  - IMU mounting movement, bad sensor read timing, or incorrect axis mapping

Keep a tuning log in `docs/` (date, change, observed behavior). Small, recorded changes beat random tweaking.

---

## Demo Media Placeholders (Add Your Own Files)

Put real bench evidence in `media/` and link it here once you have it:
- `media/bringup-open-loop.mp4` — motors + encoders open-loop verification
- `media/imu-angle-sanity.mp4` — showing tilt vs. angle readout
- `media/first-balance-attempt.mp4` — first stable upright attempts (restrained)
- `media/final-tuning-walkthrough.mp4` — your final parameters and behavior

---

## Official References

- STM32Cube documentation: https://www.st.com/en/development-tools/stm32cubeide.html  
- ST motor control resources: https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html

---

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/  
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/  
- Tutorial (checklist): https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/  
- Tutorials hub: https://feigen8n.online/tutorials/

---

## Notes / Disclaimer

Kit contents, wiring, and firmware vary by seller and revision. This repository emphasizes **verify-on-your-build** validation steps and safe bring-up order. Do not paste secrets or credentials into logs, screenshots, or commits.
