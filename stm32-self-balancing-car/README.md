# STM32 Self‑Balancing Car — Bring‑Up & PID Calibration Checklist (Verify on Your Build)

This repository is a technical, checklist‑style bring‑up guide for a **two‑wheel STM32 self‑balancing robot car** build that typically involves an **IMU for attitude sensing**, **encoders for wheel feedback**, and **PID control loops**. The purpose is to help you move from “assembled hardware” to a repeatable baseline where you can **validate wiring and sensor signals**, confirm **motor/encoder direction**, and then run **safe, incremental tuning**.

Because self‑balancing platforms are sold in many revisions (and are often re‑labeled or substituted by sellers), treat every step here as **passed only after you confirm it on your own kit**. If something in your build differs (board variant, IMU model, pinout, motor driver, encoder wiring), adjust the checks accordingly.

---

## What this repo is (and is not)

**This repo is:**
- A practical **bring‑up sequence** that prioritizes safety and observability.
- A set of **pass/fail checks** to catch common sign, axis, and wiring mistakes before tuning.
- A suggested way to organize docs, logs, and per‑build notes for reproducible iteration.

**This repo is not:**
- A claim that any specific kit revision is “supported” or verified end‑to‑end.
- A guarantee of exact parts, pin mappings, or performance on your hardware.
- A replacement for the documentation of your specific controller board, IMU, or motor driver.

---

## Quick start (recommended reading order)

If your repository includes these files, this sequence keeps troubleshooting focused:

1) `docs/setup-checklist.md` — overall bring‑up flow (power → sensors → motors → control readiness)  
2) `docs/imu-verification.md` — axis/sign sanity checks and tilt tests  
3) `docs/motor-encoder-verification.md` — direction mapping and encoder polarity  
4) `docs/pid-tuning.md` — conservative tuning workflow and logging template  
5) `docs/troubleshooting.md` — symptom → likely cause → next check  

If those files don’t exist yet, this README still stands on its own; consider using the “Repository layout” section below as a target structure.

---

## Validation stance (read this first)

- **Hardware validation:** Not claimed. No end‑to‑end hardware test coverage is asserted here.
- **What’s “validated” in spirit:** The workflow style—measure first, control later; confirm signs; clamp outputs; iterate with logs.
- **Your responsibility:** Verify voltages, polarity, sensor signs, and wheel direction on your bench before progressing.

---

## Recommended repository layout (optional, but makes collaboration easier)

A predictable structure helps you keep bring‑up notes, troubleshooting findings, and tuning experiments reviewable:

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
│   ├── photos/                # add your build photos
│   ├── videos/                # add your demo clips
│   └── logs/                  # add your UART/printf logs
└── templates/
    ├── build-log.md           # per-build record template
    └── pid-notes.csv          # gains & observations table
```

Keep any “media/” references strictly as **optional placeholders** until you actually add real files from your build.

---

## Setup notes (bench first, safe defaults)

**Workspace**
- Use a stable, non‑conductive surface.
- Secure the chassis so the wheels can spin freely during early checks.
- Have a reliable flash + debug path (and a quick way to disable motors).

**Power & safety**
- Start with wheels off the ground. Only move to floor tests after sensor and direction checks are clean.
- If you have a bench supply, use conservative current limits for first power‑ups.
- Prefer a firmware “arming” flow: read sensors first, then explicitly enable motor output.

**Assumptions (keep them minimal)**
- Many kits of this type include: an STM32 control board (or STM32‑based module), an IMU module, motor drivers, and geared DC motors with encoders.
- Exact **IMU model**, **pinout**, **driver topology**, and **firmware configuration** can vary—verify your specific revision.

---

## Bring‑up checklist (pass/fail, one line per check)

### 1) Power integrity (before flashing)
- [ ] **Polarity:** Supply polarity matches the board input markings.
- [ ] **Grounding:** Controller, motor driver, and sensors share a solid common ground.
- [ ] **Rails present:** Logic rails are stable at idle (confirm the expected voltages for your board).
- [ ] **No reset loop:** Power‑on is stable under no‑load conditions (no repeated brownout resets).

If any item fails, stop and fix power integrity before involving motors or control loops.

### 2) IMU bring‑up (sensor sanity before control)
With the robot stationary:
- [ ] **Accelerometer sanity:** Gravity is dominant on one axis at rest; readings change predictably when you tilt.
- [ ] **Gyro baseline:** Gyro is near a stable baseline when not moving (some noise/drift is normal; look for obviously wrong offsets).
- [ ] **Axis mapping:** Tilting forward/back changes the sign of the pitch‑related signal you intend to use for balancing.
- [ ] **Mounting is rigid:** The IMU is mechanically secured (avoid loose mounting during tuning).
- [ ] **Filtering feels reasonable:** If filters are enabled, noise reduces without multi‑second lag (verify via quick tilt and release).

If the IMU axes/signs are wrong, PID tuning will look random. Fix the coordinate/sign convention first.

### 3) Motor direction mapping (no balancing yet)
With wheels off the ground and very small commands:
- [ ] **Left forward:** “Forward” command spins the left wheel in your defined forward direction.
- [ ] **Right forward:** “Forward” command spins the right wheel in the same forward direction.
- [ ] **Basic symmetry:** Similar commands produce broadly similar wheel speeds (fine mismatch is OK at this stage).
- [ ] **Stop is reliable:** Zero command stops both motors predictably.

If any motor direction is inverted, decide where to fix it (wiring vs. firmware abstraction layer) and document it in `docs/wiring-notes.md`.

### 4) Encoder feedback (must match motor direction)
Spin each wheel by hand:
- [ ] **Counts change:** Encoder counts update when the wheel rotates.
- [ ] **Sign matches direction:** Forward wheel motion produces forward‑positive encoder delta (per your definition).
- [ ] **No dropouts:** Counts don’t freeze, jump wildly, or intermittently disappear during smooth rotation.
- [ ] **Left/right consistency:** Similar physical motion yields comparable magnitude on both sides.

Encoder polarity errors often masquerade as “bad tuning.” Re‑check encoder sign any time you change wiring or swap motor leads.

### 5) Control loop readiness (still not balancing)
- [ ] **Timing stability:** Control loop period is stable (verify via logs/timestamps if available).
- [ ] **Output clamped:** Motor output is limited to a safe maximum during early tests.
- [ ] **Failsafe behavior:** If IMU data is invalid or out of range, motors disable or ramp down safely.
- [ ] **Disable path works:** You can reliably stop motors immediately (software and/or hardware).

Only proceed to closed‑loop tests when these safety checks pass.

---

## PID tuning workflow (incremental, observable, reversible)

This is a safe, implementation‑agnostic tuning order. Adapt the details to your firmware architecture.

### Step A — Define signals and sign conventions
Write down (in a build log):
- What you consider **positive pitch** (lean direction).
- What you consider **forward wheel motion**.
- What the controller should do when the robot leans (which wheel direction should bring it back under the center of mass).

Then do a **manual tilt test with wheels off the ground**:
- Tilt forward slightly and observe whether the commanded motor direction would “drive under” the robot (based on your sign convention and logs/telemetry).

If the sign is wrong, PID values cannot fix it—correct signs first.

### Step B — Start with conservative limits
- Keep motor output limits low enough that the robot cannot launch off the bench.
- Prefer output ramps over steps if your firmware supports it.
- Keep an easy “disable motors” mechanism at hand during every test.

### Step C — Tune the balance (angle) loop first
Goal: responsive correction without sustained oscillation.
- Increase **P** gradually until the robot attempts to correct tilt promptly.
- Add a small **D** to reduce overshoot and high‑frequency wobble.
- Keep **I** at zero (or minimal) early to avoid slow wind‑up and surprises.

Pass criteria (supported test):
- When lightly supported, it pushes back toward upright without continuous oscillation.

### Step D — Add encoder‑based behavior (velocity/position)
After angle control is stable:
- Use encoder feedback to reduce drift and improve “stand in place” behavior.
- Re‑confirm encoder sign after any refactor (a sign error often looks like “it tries to balance while accelerating away”).

Pass criteria:
- With support, it does not continuously accelerate forward/backward while attempting to balance.

### Step E — Log every change
Use a build log (`templates/build-log.md`) and record:
- Firmware configuration snapshot (whatever you can capture on your build).
- Gain values and output limits.
- Test condition (wheels off ground / supported / cautious floor attempt).
- Observed behavior (oscillation, saturation, direction of drift).

This turns tuning into an evidence‑based process instead of guesswork.

---

## Troubleshooting (symptom → likely cause → next check)

**Symptom: immediate full‑speed output on enable**
- Likely cause: IMU angle sign wrong, motor direction mapping wrong, or output not clamped.
- Next check: disable motors; confirm IMU sign with manual tilt; confirm output clamp path.

**Symptom: violent oscillation near upright**
- Likely cause: P too high, D too low, sensor noise too high, or timing jitter.
- Next check: reduce P; add D gradually; verify loop period stability and sensor filtering.

**Symptom: balances briefly but drifts and accelerates away**
- Likely cause: encoder sign mismatch, velocity loop too aggressive, or unhandled bias.
- Next check: verify encoder polarity by hand spin; reduce velocity/position gains; inspect bias/offset handling.

**Symptom: one wheel consistently fights the other**
- Likely cause: left/right mapping mismatch, encoder channel swap, mechanical friction mismatch.
- Next check: confirm left/right direction conventions; compare encoder deltas at equal command; inspect binding.

**Symptom: works on bench, fails on floor**
- Likely cause: torque/current limits, wheel slip, different friction/loading, or saturation.
- Next check: inspect saturation during floor attempts; validate power delivery under load; check alignment and traction.

---

## Optional “media/” checklist (add only what you actually captured)

If you choose to document your build, these are useful artifacts:
- `media/photos/` — wiring overview, IMU mounting orientation, controller board close‑ups  
- `media/videos/` — supported balancing attempt, short cautious floor attempt  
- `media/logs/` — UART logs that include loop timing and sensor snapshots  

Treat these as **documentation aids**, not as proof of universal compatibility.

---

## Official references (authoritative starting points)

- STM32CubeIDE (ST official): https://www.st.com/en/development-tools/stm32cubeide.html  
- ST motor control ecosystem overview (ST official): https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html  

---

## Related links (kit, product, tutorial)

These pages may provide your baseline specs and revision notes—verify what you received matches what’s described:

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/  
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/  
- Tutorial: https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/  
- Tutorials hub: https://feigen8n.online/tutorials/
