---
status: draft
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: true
publish_target: WordPress
primary_keyword: STM32 self balancing car kit
search_intent: STM32 self-balancing robot setup, IMU checks, motor direction, PID tuning checklist
---

# STM32 self-balancing car setup and PID calibration checklist

A two-wheel balancing robot is a tight loop of **sensing → math → motor output**. When any one link is wrong (IMU axis mapping, motor direction, encoder sign, loop timing, power stability), PID tuning turns into guesswork. This tutorial is a **practical bring-up checklist** for an **STM32 self-balancing car build**, focused on *observable validation* and *safe next actions*—without assuming an exact kit revision, PCB layout, or firmware package.

If you’re evaluating the kit first, start here:

- Kit page: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- Product page: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- Tutorials hub (for related build guides): [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)

## Who this is for (and what it solves)

This guide is for:

- Builders who want a **repeatable setup workflow** before attempting balance control.
- Learners who want a **PID tuning plan** grounded in checks (not “try random gains”).
- Anyone troubleshooting a robot that **shakes, drifts, spins a wheel the wrong way, or instantly falls** on enable.

What problem it solves:

- It helps you **prove each subsystem works** (power, IMU, motors, encoders, control loop timing) before tuning.
- It gives you a structured way to **isolate sign mistakes** (a common root cause) from “real tuning.”

> Note on kit variability: even on the kit/product pages, the tutorial is framed as “checklist-style” and cautions that kit contents, wiring, and firmware steps vary by seller and revision. Treat every step below as “passed” only after *you* confirm it on your own hardware.

## What to verify before buying or building (quick reality checks)

Based on the kit/product descriptions provided in the audit context, this project is positioned around **PID control**, **IMU attitude sensing**, and **encoder motor feedback**. Before you invest time in assembly or firmware work, verify your specific kit/revision actually supports the workflow:

### 1) Control and sensing basics
- You have an **STM32-based controller** (or an STM32 module integrated on the control board).
- You have an **IMU sensor** physically present on the board or module.
- You can identify how the IMU connects (commonly I²C or SPI) *on your board*.

### 2) Actuation and feedback
- You have **two motors** mounted on a rigid frame.
- You have **encoder feedback** available (integrated motor encoders, or encoder outputs routed to the controller).
- You can locate motor driver outputs and encoder signal inputs (pins, connectors, labels).

### 3) Practical bring-up readiness
- You can power the system in a controlled way (bench supply, current limiting, or a safe battery setup).
- You can connect the controller for programming/debugging (your board’s supported method).

If any of the above is unclear from your physical kit, pause and map it first—balancing control is unforgiving about unknowns.

## Safety and bench setup (do this before any motor test)

A balancing robot can unexpectedly slam to full duty if signs are wrong. Use a bench approach that limits risk:

- Work on a **clear bench** with the robot restrained.
- For the first motor tests, keep wheels **off the ground** (a stand, blocks, or a jig).
- Use **low power** and avoid high duty cycles until direction and encoder signs are verified.
- Keep one hand ready to **cut power** immediately.

## Tools and software you’ll likely use

This guide avoids assuming a specific firmware repo or vendor package. For STM32 development, the official reference in the provided context is:

- [STM32Cube documentation / STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)

If your revision uses motor-control tooling or you want ecosystem pointers, the official reference provided is:

- [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

Typical hardware tools (choose what fits your setup):
- A stable power source (battery or bench supply), wiring tools, and basic hand tools for mechanical checks.
- A way to observe behavior: serial logs, LEDs, or other minimal debug outputs available on your board.

## Step-by-step setup workflow (bring-up checklist)

### Step 1 — Mechanical assembly sanity (before wiring)
Goal: remove “wobble causes wobble” failures.

- Frame is rigid: no loose standoffs or flex where the IMU board sits.
- Wheels are secure and aligned; shafts don’t slip under load.
- Center of mass looks reasonable: heavy battery/parts aren’t mounted extremely high or far forward.
- Cable routing doesn’t rub wheels and won’t tug on the IMU or encoder leads.

**Checkpoint (pass/fail):** when you push the chassis gently, nothing rattles, and both wheels rotate freely without scraping.

### Step 2 — Identify your coordinate system (write it down)
Balancing succeeds faster when you define “positive” directions up front.

Define these for your build (your labels, your reality):
- **Pitch angle positive**: nose up or nose down?
- **Motor positive PWM**: wheel forward or backward?
- **Encoder positive counts**: wheel forward rotation increases or decreases counts?

**Checkpoint:** you can say, in one sentence each, what “positive pitch,” “forward motor,” and “forward encoder” mean on your specific robot.

### Step 3 — Power integrity check (no motors yet)
Goal: confirm the controller and IMU can run stably without motor noise.

- Power on with motors disabled (unplug motor power, or keep duty at zero).
- Confirm the board boots reliably (no repeated resets).
- Confirm you can communicate (serial output, debugger attach, or your board’s chosen method).

**Checkpoint:** stable boot and stable logging/debug connection for at least a minute.

### Step 4 — IMU communication check (prove you can read raw data)
Goal: ensure the IMU is alive and your bus config is correct.

What to do:
- Read raw accelerometer and gyroscope values at a steady rate.
- Keep the robot stationary for 5–10 seconds, then tilt it slowly forward/backward.

What you should observe (qualitative, not numeric):
- Stationary readings look relatively steady (some noise is normal).
- Tilting changes axes consistently and repeatably.

**Checkpoint:** you can reliably detect “tilt forward vs tilt backward” in the raw IMU data without guessing.

### Step 5 — IMU axis mapping and sign (common failure point)
Goal: ensure the “pitch angle” you compute matches physical motion.

If you compute pitch angle (via a complementary filter or other method), validate it like this:

- Put the robot on a stand.
- Tilt it forward by a small angle and hold.
- Confirm your computed pitch changes in the correct direction (your chosen sign convention).

If it’s reversed or uses the wrong axis:
- Fix axis selection and sign in software first.
- Do not compensate by “weird PID gains.” PID tuning cannot fix a flipped sensor sign.

**Checkpoint:** when you tilt forward, pitch changes in the expected direction every time.

### Step 6 — Motor direction check (open loop, low duty)
Goal: make sure “forward command” actually spins the wheel forward.

- Command left motor only at low duty for a brief moment.
- Repeat for right motor.
- Compare against your “forward” definition.

If a motor direction is wrong:
- Fix by swapping leads *or* flipping direction in software (pick one consistent approach).
- Re-test after changes.

**Checkpoint:** “forward command” drives each wheel forward, and “reverse command” drives it backward.

### Step 7 — Encoder wiring and direction check (by hand first)
Goal: confirm encoders are readable and have correct sign.

- With motors disabled, spin a wheel by hand forward slowly.
- Observe encoder counts change smoothly.
- Spin backward; counts should change in the opposite direction.

If you see no counts:
- Confirm encoder wiring, power, and pin mapping.
- Confirm the input mode you configured matches your hardware (quadrature vs single-channel, etc.).

If counts change but direction is flipped:
- Fix sign in software (preferred) or swap channels if appropriate for your encoder scheme.

**Checkpoint:** each wheel produces consistent counts; forward rotation yields positive counts per your definition.

### Step 8 — Closed-loop prerequisites (timing and saturation)
Goal: prevent “it explodes on enable” due to timing errors or unlimited output.

Before enabling balance control:
- Decide a fixed control loop rate (consistent timing matters more than speed at first).
- Add output limits so PWM cannot instantly jump to max.
- Add an emergency disable condition (angle too large, comms lost, etc.) if your setup supports it.

**Checkpoint:** you can run the control loop (with output clamped to zero) and see stable timing/logs.

### Step 9 — First balance enable: “soft start” strategy
Goal: test the sign of the control action with minimal energy.

- Keep the robot supported (hands-on, stand, or a safety rig).
- Enable balance with very conservative limits.
- Observe the immediate response to a small tilt.

What you want:
- If you tip forward slightly, the wheels should try to drive in the direction that would push the robot back under its center of mass (intuitively “catching” the fall).

If it accelerates the fall:
- Stop immediately.
- This usually means **a sign error** (pitch sign, motor direction, or control output sign), not “bad gains.”

**Checkpoint:** for small manual tilts, the control action appears to oppose the tilt rather than amplify it.

## PID tuning checklist (practical, repeatable workflow)

A balancing robot often uses a combination of angle and angular velocity (or angle + gyro) feedback; your implementation may be framed as PID on angle, PD on angle, or a cascaded structure. Regardless of structure, use a disciplined process:

### 1) Start with P (proportional) only
- Set I = 0, D = 0 (or disable integrator and derivative terms).
- Increase P gradually until the robot begins to “fight back” noticeably.
- Stop increasing when you see fast oscillation or aggressive jitter.

**Validation checkpoint:** the robot responds to tilt with corrective motion, but does not immediately break into high-frequency oscillation.

### 2) Add D (derivative) to reduce overshoot and oscillation
- Increase D gradually to damp oscillations.
- If D makes the system noisy or twitchy, your gyro signal may need filtering or your loop timing may be inconsistent.

**Validation checkpoint:** oscillations reduce and the response becomes more controlled without excessive noise.

### 3) Add I (integral) only after P/D are stable
Integral is for slow biases (slight tilt offset, minor imbalance, friction differences), not for “making it balance.”

- Increase I slowly.
- Add integral limits to prevent windup (especially when the robot is held or saturated).
- If the robot slowly ramps into runaway, suspect windup or sign issues.

**Validation checkpoint:** the robot holds near upright longer and resists slow drift, without building up runaway torque.

### 4) Re-check signs anytime behavior is “backwards”
PID tuning assumes the control action is correct. If you see:
- “It always drives the wrong way when falling”
- “One wheel always runs away”
- “Balancing only works if I set negative P”

Treat that as a sign/axis/encoder convention problem, not a tuning trick.

## Validation checkpoints (what “good progress” looks like)

Use these milestones so you don’t get stuck endlessly tweaking gains:

1) **IMU readable and stable**: tilt produces consistent sign-correct changes.  
2) **Motors obey direction commands**: left and right match your forward definition.  
3) **Encoders readable and sign-correct**: forward rotation increases counts as expected.  
4) **Control loop stable with output clamped**: timing is consistent and logs are sane.  
5) **Soft enable resists tilt**: small tilts are opposed, not amplified.  
6) **P-only can “catch” briefly**: even if it oscillates, it tries to balance.  
7) **PD reduces oscillation**: response becomes calmer and less bouncy.  
8) **I reduces slow drift**: only after PD is stable.

## Troubleshooting (symptom → likely cause → what to try)

### Symptom: instantly shoots forward/backward at enable
Likely causes:
- Pitch sign is flipped
- Motor direction is inverted
- Control output sign is inverted

Try:
- Disable and verify Step 2 (sign conventions) and Step 5 (IMU mapping)
- Re-run Step 6 (motor direction) with low duty

### Symptom: violent high-frequency shaking
Likely causes:
- P too high
- D too high or gyro noise dominating
- Mechanical looseness amplifying vibration

Try:
- Reduce P first, then reduce D
- Improve mechanical rigidity and cable strain relief
- Confirm consistent loop timing

### Symptom: it balances briefly, then slowly drifts and falls
Likely causes:
- Integrator windup or I too high
- Slight sensor offset or bias not handled
- Unequal motor friction or battery sag

Try:
- Reduce I; add integral limits
- Confirm angle estimate is stable when stationary
- Check that both motors respond similarly at the same low duty

### Symptom: spins in place or one wheel “runs away”
Likely causes:
- Left/right motor direction mismatch
- One encoder direction is flipped
- One encoder not reading reliably

Try:
- Re-run Step 6 per wheel and confirm both agree on forward
- Re-run Step 7 per wheel and confirm encoder sign and continuity

### Symptom: encoder counts jump or are noisy
Likely causes:
- Wiring/connection issues
- Incorrect input mode configuration for your encoder type

Try:
- Re-seat connections, shorten/secure wires, ensure proper power/ground
- Confirm the configured encoder interface matches your hardware

## Internal links (helpful next steps)

- Kit overview and ordering info: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- Product listing page: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- Browse other setup guides: [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)

## Official external references

- STM32 IDE and STM32Cube resources: [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)  
- Motor-control ecosystem resources: [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

## FAQ

### Do I need to tune PID with the wheels on the ground?
Start with safety: do the earliest checks with wheels unloaded (stand/jig) for direction and encoder verification. Final tuning must reflect real contact and friction, but only after signs and limits are correct.

### Should I use P-only first, or jump straight to PID?
Use P-only first. If P-only behaves “backwards,” adding D and I only hides the real issue (usually sign or axis mapping).

### What if my kit revision includes “app control”?
Treat remote control as optional until balance is stable. First prove IMU, motors, encoders, and the control loop behave safely with limits. Then introduce remote inputs carefully (e.g., small target offsets), watching for saturation and windup.

### How do I know if it’s a tuning problem or a sign problem?
If enabling control **amplifies** the fall, or balancing only works with “negative” gains, assume a sign/axis/motor/encoder convention problem. If it **opposes** the fall but oscillates, that’s typically tuning and damping.

### My robot balances briefly but jitters—what should I adjust first?
Reduce P slightly, then add or adjust D to damp oscillation. If D makes it noisy, look at gyro noise, filtering, and loop timing stability before pushing gains higher.

---
