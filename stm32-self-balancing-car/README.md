# STM32 Self-Balancing Car Kit — firmware + tuning notes (draft)

A technical, review-required README for a **STM32-based self-balancing robot car kit** focused on **PID control**, **IMU attitude sensing**, **encoder motor feedback**, and optional **app control** + **ultrasonic obstacle avoidance/following**.

## Validation status (as of 2026-04-30)

- This document is a **checklist-style draft** intended for human review.
- No automated system here has flashed hardware or verified real-world balance performance.
- Any “expected behavior” notes below are **diagnostic targets**, not confirmed results.

## What’s included (kit-level)

From the kit description:

- STM32-based self-balancing robot car kit + two-wheel balancing chassis
- IMU attitude sensing module
- Encoder gear motors
- Ultrasonic module
- Battery holder and wiring
- Source code and learning materials

## Safety + handling notes

- Always bench-test with wheels off the ground first (or lightly constrained) to avoid sudden acceleration.
- If anything feels reversed (tilt sign, motor direction, encoder sign), **stop and fix polarity/sign** before PID tuning.
- Power: confirm battery wiring is correct before connecting.

## Bring-up checklist (mechanical + wiring)

### 1) Mechanical sanity
- Fasteners tightened; wheels secure; chassis not flexing around the IMU mount area.
- IMU board rigidly mounted (no foam wobble) and oriented consistently (define “forward”).

### 2) Motor direction (polarity)
- Identify left/right motor.
- Confirm that a “forward” motor command produces the same physical wheel direction on both sides.
- If one wheel spins opposite, swap motor leads (or invert in firmware later—pick one method and document it).

### 3) Encoder wiring (signal validity)
- Confirm encoders report counts when wheels rotate by hand.
- Confirm counts increase/decrease consistently with wheel direction.
- If counts never change: re-check encoder connector, power, and ground continuity.

### 4) IMU wiring (power + bus)
- Confirm stable power to the IMU module.
- Confirm the firmware can read raw IMU data (at least “device present + numbers change when moved”).

### 5) Ultrasonic module (optional)
- Power and signal lines connected.
- Verify distance reading changes with a target moved in/out.

## Firmware setup (repo expectations)

This repo should ultimately contain (or link to) the following, but filenames and tooling may differ by your environment:

- `firmware/` (recommended): STM32 firmware project (source + config)
- `docs/` (recommended): wiring notes, photos, tuning logs, demo media

Minimum “ready to tune” firmware capabilities:

- Read IMU attitude-related values (raw and/or derived angle)
- Read encoder counts / speed per wheel
- Control motor PWM (and direction) per wheel
- A place to edit/control PID gains (compile-time constants or runtime commands)
- A serial/debug output mode to log: angle, target angle, motor output, encoder speed

If these aren’t present yet, add them before attempting balance.

## IMU setup checklist (practical)

- Define your sign conventions in one place:
  - “Forward tilt” angle sign (+/−)
  - Left/right wheel positive direction
- Verify IMU readings behave correctly:
  - When you tilt the chassis forward, the reported angle should move consistently in one direction.
  - When stationary, the angle should be stable (small noise is normal).

Recommended notes to capture in `docs/tuning-log.md`:
- IMU mounting orientation (arrow/edge facing forward)
- Any offsets applied (if you use them)
- Sampling rate used (if known)

## Encoder + motor feedback checks

Before balance tuning, confirm the platform can do controlled wheel motion:

- Command a low, fixed PWM and observe each wheel spin smoothly.
- Log encoder speed and confirm it scales with PWM.
- Confirm the control loop can slow/stop wheels reliably (no “sticky start” surprises).

## PID calibration checklist (balance-first workflow)

This is a **checklist for iterative tuning**, not a promise of a specific algorithm.

### Step A — lock down the target angle
- Decide your “upright” target (often near the mechanical center of mass).
- Add a small deadband (optional) so tiny angle noise doesn’t cause constant twitching.

### Step B — start with conservative gains
- Begin with only **P** (I = 0, D = 0).
- Increase P slowly until the robot *tries* to correct tilt but does not oscillate violently.

Diagnostic targets:
- Too low P: falls over with weak correction.
- Too high P: rapid oscillation / buzzing / wheel chatter.

### Step C — add D to reduce oscillation
- Introduce **D** in small steps to dampen overshoot.
- If D is too high: response becomes jittery / noisy (often amplifies measurement noise).

### Step D — add I only if needed
- Use **I** to correct long-term bias (e.g., it “leans” and slowly drifts).
- Keep I small; watch for slow growing oscillations or runaway.

### Step E — integrate encoder feedback (speed/position) carefully
If you add a speed/position term (often used to prevent drifting), do it after basic balance is stable:

- Confirm the sign: if it “runs away,” the speed loop is likely inverted.
- Add speed correction gently; too aggressive speed control can destabilize balance.

### Step F — document one change at a time
For each tuning iteration record:
- Gains changed (P/I/D and any speed term)
- Symptom observed (oscillation frequency, drift direction, jitter)
- Battery level / surface type (these can change behavior)

## Optional features checklist

### App control support (optional)
- Define what “app control” means in your firmware:
  - Setpoint angle trim?
  - Speed/turn commands?
  - Mode switching?
- Add a safety timeout: if control packets stop, revert to neutral.

### Ultrasonic obstacle avoidance / following (optional)
- Treat ultrasonic behaviors as a *higher-level* layer:
  - Do not let obstacle logic directly break the balance loop timing.
  - Convert distance behavior into a gentle speed setpoint rather than raw motor overrides.

## Demo media placeholders (add real files later)

Create a simple, reviewable media set under `docs/media/`:

- `docs/media/bench-photo.jpg` — bench photo (kit assembled)
- `docs/media/balance-demo.mp4` — first stable balance attempt (short clip)
- `docs/media/encoder-test.mp4` — wheels off-ground, encoder + direction test
- `docs/media/ultrasonic-demo.mp4` — obstacle avoid/follow (if used)

When adding media, also add:
- `docs/media/README.md` — what each clip demonstrates and which firmware revision/gains were used.

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial topic: **STM32 self-balancing car setup and PID calibration checklist** (slug: `stm32-self-balancing-car-setup`)
