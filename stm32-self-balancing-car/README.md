# STM32 Self-Balancing Car — Setup & PID Calibration Checklist (Verify-On-Your-Build)

This repository is a technical, checklist-style bring-up guide for a **two-wheel STM32 self-balancing robot car** build that uses **IMU attitude sensing**, **encoder motor feedback**, and **PID control**. The goal is to help you move from “assembled hardware” to a repeatable baseline where you can **verify wiring + sensor signals**, confirm **motor/encoder direction**, and then perform **safe, incremental PID tuning**.

Kit contents, wiring, and firmware steps vary by seller and revision—treat each step as **passed only after you confirm it on your own hardware**.

---

## Project purpose

A balancing robot is unforgiving: one swapped motor lead, an inverted IMU axis, or encoder polarity mismatch can turn “PID tuning” into random thrashing. This repo focuses on:

- Establishing a **known-good electrical baseline** (power, grounds, connectors, polarity).
- Verifying **IMU data sanity** (axes, signs, noise, mounting orientation).
- Verifying **encoder feedback sanity** (counts change, sign, symmetry left/right).
- Confirming **motor direction mapping** (commanded direction matches physical wheel direction).
- Providing a **structured PID tuning path** that starts with conservative limits and observable tests.

---

## Validation status (read this first)

- **Hardware validation:** Not claimed. This repo does **not** assert that any specific kit revision has been tested end-to-end.
- **What is validated here:** The logic of the checklist format and the “verify-on-your-build” workflow approach.
- **Your responsibility:** Confirm every measurement (voltage, polarity, sensor sign, wheel direction) on your own bench before progressing.

---

## Recommended repository structure

This README is designed to work even if your local copy has a different layout. If you want a predictable structure for collaboration and pull requests, use this target layout:

```
.
├── README.md
├── docs/
│   ├── setup-checklist.md
│   ├── wiring-notes.md
│   ├── imu-verification.md
│   ├── motor-encoder-verification.md
│   ├── pid-tuning.md
│   └── troubleshooting.md
├── media/
│   ├── photos/                # real build photos (add yours)
│   ├── videos/                # demo clips (add yours)
│   └── logs/                  # UART/printf logs (add yours)
└── templates/
    ├── build-log.md           # per-build record template
    └── pid-notes.csv          # gains & results table template
```

If you do not plan to add files yet, keep the structure section anyway—it documents where future content should live.

---

## Setup notes (bench-first, safe defaults)

**Workspace + tools**
- Use a stable, non-conductive work surface and secure the chassis so wheels can spin freely.
- Prepare a way to observe firmware output (for example, UART logs) and a way to reflash quickly.
- Use conservative current limits on your bench supply if available, especially on first power-up.

**Power & safety**
- Never start with the robot standing upright. Begin with the wheels off the ground, then progress to a “supported balancing” test.
- If your firmware supports it, enable a “motor disable” or “arming” step so you can read sensors without driving motors.

**Assumptions (do not over-assume)**
- Your kit includes an STM32 controller board, an IMU, and encoder motors (as described on the kit/product pages).
- Board pinouts, IMU model, motor driver type, and firmware configuration are **not assumed** here—verify your specific revision.

---

## Wiring + firmware verification checklist (pass/fail, one line per check)

### 1) Power integrity (do this before flashing)
- [ ] **Polarity check:** Battery/bench supply polarity matches board input markings.
- [ ] **Ground integrity:** Common ground exists between controller, motor driver, and sensor modules.
- [ ] **Regulators:** Logic supply rails are present and stable at idle (verify your expected voltage levels on your build).
- [ ] **Brownout behavior:** Power-on does not repeatedly reset under no-load conditions.

### 2) IMU bring-up (sensor sanity before control)
With the robot stationary on the bench:
- [ ] **Static accelerometer sanity:** One axis magnitude is dominant when resting; values change predictably when you tilt the chassis.
- [ ] **Gyro zero-rate:** Gyro readings are near a stable baseline when not moving (expect some noise/drift; look for “obviously wrong” offsets).
- [ ] **Axis orientation:** Tilting forward/backward produces a consistent sign change on the pitch-related signal you use for balancing.
- [ ] **Mounting stability:** IMU board is mechanically secure; no loose tape-only mounting for final tuning.
- [ ] **Filter behavior:** If filtering is enabled, it reduces noise without adding seconds of lag (verify by quick tilt and release).

### 3) Motor direction mapping (no balancing yet)
With wheels off the ground and a very small command:
- [ ] **Left motor forward:** “Forward” command spins the left wheel in your defined forward direction.
- [ ] **Right motor forward:** “Forward” command spins the right wheel in the same forward direction.
- [ ] **Symmetry:** Similar PWM produces similar wheel speed (roughly; exact match is not required yet).
- [ ] **Stop behavior:** Zero command reliably stops both motors.

If any mapping is reversed, fix direction at the wiring or firmware abstraction layer before tuning PID.

### 4) Encoder feedback (must match motor direction)
Spin each wheel by hand:
- [ ] **Counts change:** Encoder counts increment/decrement as the wheel rotates.
- [ ] **Sign matches direction:** The sign of encoder delta matches the motor direction definition (forward wheel motion produces forward-positive feedback).
- [ ] **No dropouts:** Counts do not randomly freeze or jump when rotating smoothly.
- [ ] **Left/right consistency:** The same physical motion yields comparable magnitude on both sides.

A balancing controller that uses velocity feedback will behave badly if encoder polarity is wrong.

### 5) Control loop readiness (still not balancing)
- [ ] **Timing stability:** Control loop runs at a stable period (verify with logs/timestamps if available).
- [ ] **Saturation limits:** Motor output is clamped to a safe maximum during early tests.
- [ ] **Fail-safe:** If IMU data becomes invalid, motors are disabled (or safely ramped down).

---

## PID tuning workflow (incremental, observable, reversible)

This section describes a safe tuning order and what “good” looks like. It does not assume a specific firmware implementation.

### Step A — Define your signals and signs
Before changing gains, write down:
- The angle signal used for balance (for example, pitch estimate).
- The sign convention for “lean forward” and “wheel forward”.
- The direction the controller should drive the wheels when the robot leans.

Then do a **manual tilt test** with wheels off the ground:
- Gently tilt the robot forward; confirm the controller would command wheel motion that would move under the center of mass (verify on your build).

If the sign is wrong, no PID value will fix it.

### Step B — Start with conservative limits
- Set motor output limits low enough that the robot cannot launch off the bench.
- Prefer ramping outputs rather than step changes if your firmware supports it.

### Step C — Tune the balance (angle) loop first
Goal: get a “stiff but not violent” response.
- Increase **P** gradually until the robot attempts to correct tilt promptly.
- Add a small **D** to reduce overshoot and oscillation.
- Keep **I** at zero or very small initially to avoid slow wind-up that causes surprise runaways.

Pass criteria (supported test):
- When lightly supported, the robot pushes back toward upright without sustained oscillation.

### Step D — Add velocity/position behavior (using encoders)
Once angle control is stable:
- Use encoder feedback to reduce drift and improve “stand-in-place” behavior.
- Confirm encoder sign again after any refactor: a sign error here often looks like “it tries to balance while accelerating away”.

Pass criteria:
- The robot does not continuously drive forward/backward while trying to balance (with support).

### Step E — Iterate with a build log
Record every change:
- Firmware version/config snapshot (whatever you can capture for your build).
- Gain values.
- Test condition (wheels off ground / supported / free-standing attempt).
- Observed behavior (oscillation frequency, direction, any saturation).

This makes tuning reviewable and reproducible.

---

## Troubleshooting (symptom → likely cause → next check)

**Symptom: immediate full-speed spin on enable**
- Likely cause: IMU angle sign wrong, motor direction mapping wrong, or output not clamped.
- Next check: disable motors; verify IMU sign with a manual tilt; confirm output clamp.

**Symptom: violent oscillation around upright**
- Likely cause: P too high, D too low, or control loop timing unstable.
- Next check: reduce P; increase D slightly; verify loop period stability.

**Symptom: balances briefly but drifts and accelerates away**
- Likely cause: encoder sign mismatch, velocity loop too aggressive, or unhandled bias.
- Next check: verify encoder polarity with hand spin; reduce velocity-related gains; check sensor bias handling.

**Symptom: one wheel consistently fights the other**
- Likely cause: left/right motor mapping mismatch, encoder channel swap, mechanical friction mismatch.
- Next check: confirm left/right directions; compare encoder deltas at equal command; check for binding.

**Symptom: works on bench, fails on floor**
- Likely cause: insufficient torque/current, wheel slip, different friction/loading, or output saturation.
- Next check: inspect saturation; verify power delivery under load; confirm mechanical alignment and wheel traction.

---

## Demo media placeholders (add real files when you have them)

- `media/photos/bench-overview.jpg` — full kit bench photo (your build)
- `media/photos/imu-mount-closeup.jpg` — IMU mounting orientation reference (your build)
- `media/videos/first-balance-supported.mp4` — supported balancing clip (your build)
- `media/videos/free-standing-attempt.mp4` — short free-standing attempt (your build)
- `media/logs/control-loop-uart.txt` — UART log snippet showing loop timing and sensor readouts (your build)

Do not treat placeholders as proof of validation; only add files that you actually captured.

---

## Official references

- STM32Cube documentation (STM32CubeIDE): https://www.st.com/en/development-tools/stm32cubeide.html  
- ST motor control resources: https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html  

---

## Related (product + tutorial)

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/  
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/  
- Tutorial: https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/  
- Tutorials hub: https://feigen8n.online/tutorials/
