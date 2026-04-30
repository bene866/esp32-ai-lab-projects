# STM32 Self-Balancing Car Kit — Setup & PID Calibration Checklist (Repo Draft)

A hands-on STM32 self-balancing robot car project for learning **PID control**, **IMU attitude sensing**, and **encoder motor feedback**, with optional **app control** and an **ultrasonic** module for simple obstacle-avoidance / following experiments.

## Validation Status (as of 2026-04-30)

This README is a **technical-first draft**. It does **not** claim any verified hardware testing.

| Item | Status | Notes |
|---|---:|---|
| Firmware builds | Not verified | Add exact toolchain + command once confirmed |
| Flash / program | Not verified | Add programmer + steps once confirmed |
| IMU data stable at rest | Not verified | Requires bench check + logging |
| Encoder counts correct direction | Not verified | Requires wheel spin test |
| Balance on stand (wheels off ground) | Not verified | Safer first PID bring-up step |
| Balance on floor | Not verified | Requires tuned PID + safety checks |
| App control | Not verified | Add app + protocol details after confirmation |
| Ultrasonic avoid/follow mode | Not verified | Add wiring + thresholds after confirmation |

## What’s Included (Kit-Level)

- STM32-based self-balancing robot car kit
- Two-wheel balancing chassis
- IMU attitude sensing module
- Encoder gear motors
- Ultrasonic module
- Battery holder and wiring
- Source code and learning materials

## Safety Notes (Read Before Power-On)

- Do first tests **with wheels off the ground** (stand/block the chassis).
- Keep a **kill-switch** ready (battery unplug / power switch) and avoid loose wiring near wheels.
- Start with **low motor output limits** and **short test windows** to avoid runaway oscillation.

## Bring-Up Checklist (No Assumed Pinout)

Use this section as a **repeatable checklist**. Fill in the specifics (MCU model, pins, timer channels, IMU type, etc.) after confirming the actual hardware + code.

### 1) Mechanical / Assembly Sanity

- Verify both wheels spin freely; chassis is symmetric; battery is secured.
- Confirm IMU is mounted firmly and oriented consistently (define **IMU frame** vs **robot frame**).
- Confirm encoder disks/sensors are aligned; no intermittent contact.

### 2) Power & Basic Electrical

- Confirm battery polarity and connector orientation.
- Confirm motor driver wiring is correct (left/right mapping).
- Confirm IMU and ultrasonic modules have correct power rails and stable ground reference.

### 3) Firmware Minimum Features (Stage-Gated)

Target incremental milestones:

- **Stage A — Sensors only:** read IMU angle estimate + raw gyro/accel; read encoder counts.
- **Stage B — Motors only:** open-loop motor drive with strict limits (no balance control).
- **Stage C — Balance on stand:** closed-loop angle stabilization with output clamps.
- **Stage D — On-floor balance:** add speed/position loop (encoders) only after angle loop is stable.
- **Stage E — Extras:** app control + ultrasonic behavior modes.

## IMU Setup Notes (Practical, Hardware-Agnostic)

### Define the “Balance Axis”
- Decide which axis represents pitch (forward/back tilt) for balancing.
- Document sign conventions:
  - Positive angle direction
  - Positive motor command direction
  - Positive encoder direction

### Quick IMU Sanity Tests
- At rest, the angle estimate should be stable (low drift) over ~30–60 seconds.
- When tilting the robot forward/back by hand:
  - Angle changes smoothly
  - Direction matches your sign convention

If any of these fail, fix sign/orientation before touching PID.

## Encoder Setup Notes

### Quick Encoder Sanity Tests
- Spin left wheel forward by hand:
  - Left encoder count increases (or decreases) consistently
  - Right encoder stays mostly unchanged (minor noise is acceptable)
- Repeat for right wheel.

Document:
- Counts per wheel revolution (measured)
- Any gearing ratio assumptions used in software

## PID Calibration Checklist (Recommended Order)

This project is best tuned **inside-out**:

1) **Angle loop** (IMU → motor torque)  
2) **Speed loop** (encoders → target angle bias)  
3) **Position loop / drift correction** (optional, depends on implementation)

### Step 0 — Set Conservative Limits
- Clamp motor PWM / command output (start low).
- Add a watchdog/timeout to disable motors if sensor data stops updating.
- Add a “fallen over” threshold: if angle exceeds a safe limit, cut motors.

### Step 1 — Tune Angle P (Proportional)
- With wheels off the ground:
  - Increase `Kp_angle` until the system starts to react strongly to tilt.
  - Back off if it oscillates rapidly or saturates output continuously.

**Goal:** strong correction without sustained oscillation.

### Step 2 — Add Angle D (Derivative / Damping)
- Increase `Kd_angle` to reduce oscillation and overshoot.
- If the response becomes noisy/jittery, reduce `Kd_angle` or filter gyro/angle.

**Goal:** damped response that settles quickly after a tilt.

### Step 3 — Add Angle I (Integral) Only If Needed
- Use integral sparingly for steady-state bias (sensor bias / motor mismatch).
- Too much integral will cause slow build-up and sudden runaway.

**Goal:** correct small residual lean without slow oscillation.

### Step 4 — Introduce Speed Loop (Encoders)
Once angle loop is stable:
- Use encoder speed to adjust the target angle slightly (lean forward to move forward).
- Start with very small gains and strict clamps on angle bias.

**Goal:** control forward/back speed without destabilizing balance.

### Step 5 — Optional Position / Drift Correction
- Only after speed loop behaves.
- Keep gains tiny; prioritize stability over “perfect stillness”.

## Logging & Debug (Strongly Recommended)

Add (or enable) a simple telemetry stream (UART/USB):
- Timestamp
- Angle estimate
- Gyro rate
- Encoder counts/speed
- PID terms (P/I/D)
- Motor outputs

This makes tuning repeatable and reviewable.

## Demo Media (Placeholders)

Add real media once captured (no placeholders should be presented as proof of validation).

- `media/bench-imu-telemetry.png` — IMU angle stability at rest
- `media/stand-angle-step.gif` — wheels-off-ground angle response to hand tilt
- `media/first-balance-on-floor.mp4` — first stable balancing clip
- `media/app-control-demo.mp4` — app control (if used)
- `media/ultrasonic-avoid-demo.mp4` — avoid/follow mode (if used)

## Repository Conventions (Recommended)

If you need a clean structure, consider:

- `firmware/` — STM32 project source
- `docs/` — calibration notes, wiring tables, tuning logs
- `media/` — images/videos used in docs
- `tools/` — scripts for plotting logs / parameter sets

(Adjust to match the actual repository layout.)

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials index: https://feigen8n.online/tutorials/
- Planned tutorial slug (may not be published yet): `stm32-self-balancing-car-setup`

## Maintenance Notes (For Contributors)

- Do not merge “tuned PID values” without:
  - the exact hardware configuration (IMU type/orientation, motor/encoder details)
  - a short tuning log (what changed, why, and what improved)
- Avoid hardcoding assumptions (pins, axes, counts/rev) without documenting them in `docs/`.
