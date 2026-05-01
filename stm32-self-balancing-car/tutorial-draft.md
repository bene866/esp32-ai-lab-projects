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

A two-wheel self-balancing robot is a fast way to learn real control loops: you’re forced to make sensors, motor drive, encoder feedback, and PID control cooperate in a tight loop. This guide is a **checklist-style bring-up workflow** for an **STM32 self-balancing car kit**—focused on **IMU checks, motor direction verification, encoder sanity tests, and safe PID tuning steps**.

Because kit revisions and seller wiring vary, treat every step as **“passed” only when you can observe it on your own hardware**. Don’t assume pinouts, connector labels, IMU orientation, or motor/encoder wiring matches any particular photo or schematic unless your kit explicitly documents it.

## Who this is for (and what problem it solves)

This checklist is for:
- Builders who want a **repeatable setup flow** (instead of tuning PID while the wiring is still wrong).
- Robotics learners who want to connect “PID theory” to observable tests: angle sign, motor polarity, and feedback direction.
- Anyone deciding whether to buy/build a kit that advertises **PID control, IMU attitude sensing, encoder motor feedback, and app control**.

It solves the most common early failure mode: **trying to tune PID before the IMU, motors, and encoders are verified**.

## Quick links (internal)

- Kit page: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- Product page: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- Tutorials hub: [Tutorials](https://feigen8n.online/tutorials/)

## Before you buy: what to verify on the product page

If you’re comparing sellers or deciding whether this kit fits your goals, confirm the basics before checkout:

1) **Learning goals match the features**
- Look for explicit mention of **PID control**, **IMU attitude sensing**, and **encoder motor feedback** (these are core to balancing).
- If **app control** is mentioned, treat it as a *secondary* feature; balancing bring-up should work even without phone control.

2) **You can support the STM32 workflow**
- Ensure you have a reasonable path to build and flash firmware for your STM32-based board using tools like [STM32CubeIDE documentation](https://www.st.com/en/development-tools/stm32cubeide.html).

3) **You’re comfortable with revision variability**
- Expect that “what’s included” and wiring details can differ by kit revision. Plan to validate each subsystem (IMU, motors, encoders) independently before attempting balancing.

4) **Shipping and purchasing fit your situation**
- Review the order section on the kit/product page and any shipping notes before you commit: [kit page](https://feigen8n.online/kits/stm32-self-balancing-car-kit/) and [product page](https://feigen8n.online/product/stm32-self-balancing-car-kit/).

## Safety and setup mindset (important)

Balancing robots can suddenly accelerate when a sign is wrong. Use a workflow that reduces risk:

- **Start with wheels off the ground** (stand, blocks, or a cradle) for motor-direction and basic feedback tests.
- Add a **hard stop** concept early: a switch, a “disable motors” command, or a fast way to cut power.
- Increase power and loop gains **slowly**. If you jump straight to aggressive PID values, you’ll mix safety issues with debugging issues.

## What you’re bringing up (systems checklist)

A stable self-balancing build requires all of these to be correct:

- **IMU orientation and angle sign** (tilt forward must produce the expected sign)
- **Motor direction** (commanded “forward” must match your frame definition)
- **Encoder sign** (wheel rotation direction must match your sign convention)
- **Control loop direction** (when the robot tips forward, the wheels must drive in the direction that pushes it back under its center of mass)
- **Reasonable timing** (consistent loop period; stable sampling)
- **PID gains** (tuned last, not first)

## Tools and prep (keep it minimal)

You do not need a lab bench, but you do need a consistent way to build/flash firmware and observe signals.

- A development setup compatible with your STM32 board and [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)
- A way to log or print key values (even a basic serial output is enough): angle estimate, motor command, encoder counts/speed
- Basic hand tools for assembly and rework as needed
- A safe test stand so the wheels can spin freely during early tests

If your kit uses a dedicated motor driver or motor control approach, ST’s ecosystem page can help you navigate terminology and concepts: [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html).

## Step-by-step setup workflow (from zero to “ready to tune”)

### Step 1 — Define your coordinate system (write it down)

Before you wire anything, define these conventions:

- **Forward direction**: which way the robot “front” points
- **Pitch angle sign**: what sign you expect when the robot tips forward
- **Motor positive direction**: what “+PWM” or “+command” means for each wheel
- **Encoder positive direction**: what “+counts” means for each wheel

Write the definitions in your notes so you don’t “fix” a sign in three different places later.

**Pass condition:** you can state your sign conventions in one sentence each (forward, pitch, motor+, encoder+).

---

### Step 2 — Mechanical sanity checks (before power)

Even perfect PID can’t fix a mechanically inconsistent chassis.

- Confirm wheels spin freely without rubbing
- Check that both wheels have similar friction and no binding
- Ensure the IMU board (or sensor module) is firmly mounted and won’t shift
- Verify the center area (battery/controller stack) is secure so mass doesn’t wobble

**Pass condition:** when you spin each wheel by hand, it feels smooth and similar left vs right.

---

### Step 3 — Wiring verification (do not assume colors)

Kits often change wire colors or connector layouts across revisions. Verify by function:

- Identify motor leads for left/right motor
- Identify encoder channels for left/right encoder (if present)
- Identify IMU connection (I2C/SPI lines as applicable)
- Identify power rails and ground

If you don’t have a provided wiring map for your specific revision, label cables yourself. The goal is not perfection—just that you can *trace what is what*.

**Pass condition:** every cable is labeled left/right and “motor/encoder/IMU/power”, even if pin names are unknown.

---

### Step 4 — Firmware bring-up: create a “sensor + motor test” mode

Before you attempt balancing, create or enable a firmware mode that can run three independent tests:

1) **IMU readout test** (raw or computed angle)
2) **Motor spin test** (manual control with low power)
3) **Encoder readout test** (counts change when wheel turns)

Use [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) as your central workflow for building and flashing firmware.

**Pass condition:** you can flash firmware repeatedly and see some form of output that confirms the program is running (LED, serial log, etc.).

---

### Step 5 — IMU checks: orientation, stability, and sign

Balancing depends on correct tilt feedback. Validate your IMU step-by-step:

#### 5.1 Confirm the IMU is “alive”
- Verify the IMU responds over its bus (I2C/SPI)
- Print or log a basic stream (raw accel/gyro, or a computed pitch angle)

**Pass condition:** values change when you move the robot and are not stuck.

#### 5.2 Confirm “pitch” moves the way you think
- Hold the robot upright and still: observe baseline
- Tilt forward slowly: confirm pitch changes smoothly
- Tilt backward: confirm it changes in the opposite direction

If the sign is reversed, do **one** correction (either swap sign in software or redefine your sign convention). Avoid applying sign flips in multiple layers.

**Pass condition:** “tilt forward” consistently produces the expected sign and direction in your logs.

#### 5.3 Confirm noise and drift are reasonable
You don’t need perfection yet, but you should detect obvious problems:
- If values jump violently while stationary, suspect wiring/grounding or loose mounting
- If the sensor saturates or clips unexpectedly, suspect configuration issues

**Pass condition:** stationary readings are relatively stable and repeatable.

---

### Step 6 — Motor direction test (wheels off the ground)

Do this on a stand so you can safely observe direction.

- Command a small forward drive on the **left motor only**
- Confirm the left wheel turns in your defined “forward” direction
- Repeat for the right motor

If one motor direction is reversed, choose **one** method to correct it:
- Swap motor leads (hardware), or
- Reverse motor command sign (software)

**Pass condition:** left and right “forward commands” both spin their wheels forward relative to your frame.

---

### Step 7 — Encoder direction test (counts must match wheel motion)

Encoders are your truth source for wheel rotation. Validate them without the balancing loop.

- Rotate the left wheel forward by hand: confirm left encoder count increases (or matches your encoder+ definition)
- Rotate it backward: confirm it decreases
- Repeat for the right wheel
- If you compute speed, ensure forward rotation gives positive speed

If left/right channels are swapped or sign is inverted, fix it once (swap A/B assignment in software, or adjust sign convention consistently).

**Pass condition:** each wheel’s encoder changes in the correct direction and does not cross-couple with the other wheel.

---

### Step 8 — “Control direction” test (the most important checkpoint)

This is the moment that prevents runaway behavior.

With wheels off the ground, run the balance controller with:
- **Very low motor output limit**
- A quick disable option
- Clear logging: angle and motor command sign

Then do this:

- Tilt the robot forward slightly.
- Observe motor response.

For balance to work, the wheels must respond in a way that would bring the robot back under itself (in your coordinate system). If it drives the wrong way, stop and fix sign conventions before tuning PID.

**Pass condition:** when tipped forward, the commanded wheel motion is in the stabilizing direction (not amplifying the fall).

---

### Step 9 — PID tuning checklist (slow, logged, and repeatable)

Only start tuning after Steps 5–8 pass.

A practical tuning flow:

1) **Start with P only**
- Set I = 0, D = 0
- Increase P gradually until the robot begins to “push back” toward upright
- Watch for fast oscillation (too much P) vs sluggish correction (too little P)

2) **Add D to reduce oscillation**
- Increase D gradually to dampen overshoot
- If the robot becomes jittery/noisy, D may be too high or the angle signal is too noisy

3) **Add a small I to correct steady bias**
- Use I to address consistent lean or small steady-state error
- Increase slowly; too much I causes slow “wind-up” and sudden surges after disturbances

4) **Tune limits and safety constraints**
- Motor output limit: keep low until stability is proven
- Angle cutoff: if the tilt exceeds a threshold, disable motors (to avoid chasing a fall)
- Rate limiting: avoid instant large changes that stress the drivetrain

**Pass condition:** the robot can attempt to stabilize around upright without immediately running away, and changes in P/D/I produce predictable changes in behavior.

---

## Validation checkpoints (copy/paste checklist)

Use this as a “done means done” list:

- [ ] IMU responds and updates continuously
- [ ] Tilt forward/back produces correct sign and smooth response
- [ ] Left/right motor “forward” matches chassis forward
- [ ] Left/right encoder counts match wheel direction and correct wheel
- [ ] Balance loop drives wheels in stabilizing direction when tipped
- [ ] P-only control shows correction (even if oscillatory)
- [ ] Adding D reduces oscillation without introducing jitter
- [ ] Adding small I reduces steady bias without wind-up surges
- [ ] Motor output limit and disable behavior are confirmed

## Troubleshooting (symptom → likely cause → next action)

### Symptom: Motors instantly accelerate when balancing starts
- Likely cause: control direction is wrong (angle sign, motor polarity, or encoder sign mismatch)
- Next action: repeat **Step 8** with a very low output limit and confirm stabilizing direction

### Symptom: Robot oscillates rapidly around upright
- Likely cause: P too high, D too low, or noisy angle estimate
- Next action: lower P slightly, add D gradually, and re-check IMU mounting stability (Step 2)

### Symptom: Robot barely reacts and slowly falls over
- Likely cause: P too low, motor output limit too low, or loop not running at consistent timing
- Next action: increase P carefully, confirm motors can produce enough torque at low command, and verify loop timing consistency in firmware

### Symptom: It stabilizes briefly then slowly “walks away” or leans permanently
- Likely cause: bias or steady-state error; I may be needed (or sensor offset)
- Next action: add small I, verify angle baseline when upright, and ensure “upright reference” is defined consistently

### Symptom: Encoder values look random or don’t change smoothly
- Likely cause: incorrect wiring, channel assignment mismatch, or poor signal integrity
- Next action: re-check encoder wiring labels (Step 3), re-run hand-rotation test (Step 7), and ensure left/right are not swapped

### Symptom: IMU values jump while stationary
- Likely cause: loose sensor mount, unstable power/ground, or configuration issues
- Next action: secure the IMU physically, re-check wiring and grounding, and confirm the IMU readout is stable before balancing (Step 5)

## Recommended internal links to place on related pages

If you maintain product and tutorial navigation, these link placements help users reach the checklist at the right time:

- From the kit page to this tutorial: link “STM32 self-balancing car setup and PID calibration checklist” on [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- From this tutorial back to purchase pages:
  - “Kit page” → [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
  - “Product page” → [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- From the tutorial to the hub for discovery: [Tutorials](https://feigen8n.online/tutorials/)

## Official references (external)

- STM32 IDE and workflow reference: [STM32CubeIDE documentation](https://www.st.com/en/development-tools/stm32cubeide.html)
- Motor-control ecosystem overview (concepts and resources): [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

## FAQ

### Do I need to tune PID right away?
No. First pass Steps 5–8 so you know the IMU and wheel feedback are correct. PID tuning is meaningful only after the signs and directions are verified.

### What’s the single most important test before tuning?
The **control direction test** (Step 8). If tipping forward causes the wheels to drive in the wrong stabilizing direction, no PID values will save it.

### My kit revision doesn’t match a diagram I found—what should I do?
Use this workflow as a functional checklist: identify IMU, motors, encoders, power, then validate each subsystem by observation. Revisions can differ, so treat external diagrams as hints, not truth.

### Is app control required for balancing?
Not for bring-up. App control can be useful later, but your balancing loop should be verifiable through basic tests and logs without relying on a phone feature.

### When should I increase motor power limits?
Only after the robot shows correct stabilizing behavior at low limits. Raise limits gradually while keeping a fast disable option available.

---
If you want to keep exploring related builds and guides, start from the main list: [Tutorials](https://feigen8n.online/tutorials/).
