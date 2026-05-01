---
status: publish
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: false
publish_target: WordPress
primary_keyword: STM32 self balancing car kit
search_intent: STM32 self-balancing robot setup, IMU checks, motor direction, PID tuning checklist
---

# STM32 self-balancing car setup and PID calibration checklist (safe bring-up)

A two-wheel self-balancing robot is one of the fastest ways to *feel* control theory become real: it either stands up, oscillates, or face-plants. This tutorial is a practical setup + PID calibration checklist for a typical **STM32 self-balancing car kit** that uses an **IMU** for attitude sensing and **encoder motors** for feedback.

It’s written for builders who want a safe, repeatable bring-up process with clear “pass/fail” checkpoints before spending hours tuning.

Because these kits vary by seller and hardware revision, this guide avoids assuming fixed pinouts, fixed IMU models, exact kit contents, or any single firmware layout. Treat each step as “passed” only after you verify it on *your* kit.

**Related pages**
- Kit page: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- Product page: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- Tutorials hub: [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)

---

## Table of contents

- [Who this is for](#who-this-is-for)
- [What to check before you start](#what-to-check-before-you-start)
- [Safety first (read once, follow always)](#safety-first-read-once-follow-always)
- [Bring-up workflow with checkpoints](#bring-up-workflow-with-checkpoints)
  - [Step 1 — Document your kit revision](#step-1--document-your-kit-revision-10-minutes)
  - [Step 2 — Establish a reliable flash workflow](#step-2--establish-a-reliable-flash-workflow-without-assuming-code)
  - [Step 3 — Verify power rails and ground](#step-3--verify-power-rails-and-ground-logic-vs-motors)
  - [Step 4 — Motor direction test (open-loop)](#step-4--motor-direction-test-open-loop-no-balancing-yet)
  - [Step 5 — Encoder sanity check](#step-5--encoder-sanity-check-counts-move-the-right-way)
  - [Step 6 — IMU sanity checks](#step-6--imu-sanity-checks-stillness-axes-and-sign)
  - [Step 7 — Upright reference + control sign sanity](#step-7--upright-reference--control-sign-sanity-the-make-or-break-step)
  - [Step 8 — First closed-loop tests (low-risk)](#step-8--first-closed-loop-tests-low-risk)
- [PID tuning workflow (practical, repeatable)](#pid-tuning-workflow-practical-repeatable)
- [“Ready” milestones](#ready-milestones)
- [Troubleshooting (symptom → likely cause → next action)](#troubleshooting-symptom--likely-cause--next-action)
- [References](#references)
- [FAQ](#faq)

---

## Who this is for

You’ll benefit most if you:
- Have an STM32-based balancing car kit (or compatible parts) and want a realistic bring-up plan.
- Prefer checkpoints like “IMU axis makes sense” and “motor direction is correct” before tuning.
- Want a tuning workflow that starts with safety, then progresses from “moves” to “balances”.

This checklist helps prevent common time-sinks:
- “It powers on but does nothing” (bring-up gaps).
- “Motors fight each other / wrong direction” (sign conventions and mapping).
- “It oscillates violently” (gains too aggressive or loop direction wrong).
- “It falls immediately” (IMU axis/sign errors, wrong upright reference, or control sign inverted).

---

## What to check before you start

If you’re still shopping or just unboxed a kit, verify these basics using the listing page, any included sheet/manual, and what you can physically see on the hardware. Kits are often marketed around **PID control**, **IMU-based attitude estimation**, and **encoder feedback**, but exact implementations vary.

**Quick verification checklist (validate on your kit):**
1. **Controller is STM32-based** (exact MCU can vary; don’t assume pinouts).
2. **IMU module exists and is rigidly mounted** (loose mounting = noisy readings).
3. **Motors + encoder wiring are present** (encoders may be separate connectors).
4. **Power path is clear**: what powers logic, what powers motors, and how ground is shared.
5. **You have a way to flash firmware** (ST-LINK, USB DFU, serial bootloader, or a vendor-provided method—confirm *before* you rely on it).
6. **Mechanical build is sane**: wheels spin freely, nothing rubs, wiring won’t hit moving parts.

If any of the above is uncertain, don’t guess—document what you have, then proceed step-by-step below.

---

## Safety first (read once, follow always)

Balancing robots can suddenly lurch when a control loop starts. Your goal is to eliminate avoidable risks before any closed-loop test.

**Mechanical “no-power” checks (PASS/FAIL):**
- **PASS**: Wheels spin freely by hand with minimal rubbing.
- **PASS**: Chassis is symmetric enough that both wheels touch evenly.
- **PASS**: IMU board/module is firmly fixed (no wobble, no soft tape that flexes).
- **PASS**: No exposed pads or solder joints can short against metal standoffs.
- **FAIL**: Wheel binds, IMU is floating, or wires can hit wheels. Fix first.

**Power safety setup (recommended):**
- Do the first motor and closed-loop tests with the robot **lifted off the ground** (a small box stand works).
- Start at **reduced power** if possible (lower supply voltage or a current-limited bench supply if you have one).
- Have a fast cutoff: switch, unplug, or accessible connector you can pull quickly.
- Keep fingers, hair, and loose wires away from wheels and gears.

---

## Bring-up workflow with checkpoints

Follow these steps in order. Don’t “skip ahead to PID” until you can pass the earlier checkpoints—most balancing failures are sign/mapping issues, not “mystical tuning problems”.

### Step 1 — Document your kit revision (10 minutes)

Because revisions vary, create your own “hardware map” first:
- Take photos of the assembled chassis, wiring, and board silkscreen labels.
- Note the IMU orientation: which edge faces forward, and how the PCB is mounted (flat/vertical).
- Identify likely connectors: motor outputs, encoder inputs, battery input, switch, and programming/debug header.

Optional (but very useful):
- Create a short note: “Left motor connector = ___”, “Right encoder connector = ___”, “Battery = ___”.
- Mark left/right on the chassis with tape to avoid swapping during debugging.

**Checkpoint**
- **PASS**: You can point to each connector and describe what it likely does (motor, encoder, power, programming).
- **FAIL**: You’re not sure what connects where—pause and trace wiring physically before powering anything.

---

### Step 2 — Establish a reliable flash workflow (without assuming code)

Most tuning sessions fail because flashing is unreliable or you can’t iterate quickly. Your first job is simply: *can you program the board repeatedly and predictably?*

Common official tooling entry points (choose what matches your setup):
- STM32CubeIDE: [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)
- STM32CubeProgrammer (useful for ST-LINK/DFU flashing): [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)

If your kit provides a different workflow, that’s fine—use what fits your hardware. The goal is repeatability, not a specific tool.

**Checkpoint**
- **PASS**: You can flash *something* to the board and repeat it reliably (power cycle, flash again, no drama).
- **FAIL**: Flashing is intermittent or unclear—solve this before any PID work.

---

### Step 3 — Verify power rails and ground (logic vs motors)

Balancing robots are sensitive to brownouts and electrical noise. Before running any control code:
- Confirm the logic side powers consistently (no random resets).
- Confirm the motor supply is appropriate for your motor driver and battery choice.
- Confirm grounds are connected as intended by the design (most kits share ground between logic and motor power, but don’t assume—verify your board’s labeling and wiring).

**Checkpoint**
- **PASS**: The board powers on consistently, and gentle connector movement doesn’t cause resets.
- **FAIL**: Random resets or flicker—fix power wiring/connector seating before motor tests.

---

### Step 4 — Motor direction test (open-loop, no balancing yet)

This is the most important sign-convention test. You need a way to command each motor forward/backward at low duty (via firmware test mode, a simple motor test routine, or whatever your kit provides).

**Test sequence (wheels off the ground):**
1. Lift the robot so wheels spin freely.
2. Command **left motor** slowly forward, then reverse.
3. Command **right motor** slowly forward, then reverse.
4. Define what “forward” means for your build (e.g., the robot would roll forward on the floor).

**What you’re checking**
- Each motor spins reliably at low command.
- Left/right mapping is correct (left command affects left wheel).
- Forward/reverse is consistent and repeatable.

**Checkpoint**
- **PASS**: Left/right are not swapped, and forward/reverse are consistent for both wheels.
- **FAIL**: Swapped motors, inverted direction, or intermittent rotation—fix wiring or software mapping now.

Tip: If your motor driver wiring supports swapping motor leads, that can flip direction electrically. If not, direction can usually be inverted in software. Use whichever is safer and easier to maintain for your setup.

---

### Step 5 — Encoder sanity check (counts move the right way)

Encoder feedback is commonly used for speed/velocity stabilization and for “drive forward/back” features layered on top of balance. Even if you plan to balance without motion at first, you still want encoder signals to be trustworthy before building more features.

**Hardware-agnostic test idea:**
- Rotate the left wheel forward by hand and observe encoder counts change.
- Rotate backward and confirm counts change in the opposite direction.
- Repeat for the right wheel.

**What “good” looks like**
- Counts change smoothly with motion (not stuck at zero).
- Direction sign is consistent: forward motion always changes counts the same way.

**Common pitfalls**
- Counts don’t change: wrong connector, missing wiring, pin mapping mismatch, or encoder not powered/configured.
- Counts change but direction is inverted: A/B channels swapped or sign needs inversion in software.
- Counts jump wildly: noisy wiring, weak connections, incorrect pullups, or wrong input configuration.

**Checkpoint**
- **PASS**: Both encoders change consistently with wheel motion; direction sign is understandable and repeatable.
- **FAIL**: No counts, nonsense counts, or inconsistent direction—do not tune PID until encoder readings are reliable.

---

### Step 6 — IMU sanity checks (stillness, axes, and sign)

The IMU is the robot’s sense of “upright”. Before perfect calibration, confirm these basics:

**Stillness check**
- With the robot stationary, IMU-derived angle/tilt should be relatively stable (small noise is normal; chaotic jumping is not).

**Axis + sign check**
- Tilt the robot forward/backward slowly. The reported tilt (or pitch angle) should change smoothly.
- Tilt left/right. The signal associated with roll should change (even if your control loop doesn’t use it).

Because different kits use different IMU models and filtering approaches (complementary filter, Kalman, vendor library, etc.), focus on universal observations:
- Smooth response to slow tilt.
- Repeatability: returning to the same physical pose gives similar readings.
- Consistent sign: the same physical motion changes the angle the same way each time.

**Checkpoint**
- **PASS**: Stationary readings aren’t chaotic, and tilting produces a smooth, repeatable change.
- **FAIL**: Extremely noisy or inconsistent readings—check IMU mounting rigidity, wiring, and power stability.

---

### Step 7 — Upright reference + control sign sanity (the make-or-break step)

Most “it falls instantly” failures come from one of these:
- The controller’s “upright” setpoint doesn’t match the real mechanical upright pose.
- Pitch/roll axis is swapped (you’re controlling the wrong axis).
- The control sign is inverted (it pushes *away* from upright).

**Procedure**
1. Hold the robot in its intended balancing pose (often close to vertical).
2. Observe the angle signal you intend to control (usually pitch).
3. Tilt slightly forward: confirm the angle changes in the expected direction.
4. Tilt slightly backward: confirm it changes the opposite way.

Now do a **control-direction sanity check** *without letting it run away*:
- Enable the control loop with wheels off the ground and with output limited if your firmware supports it.
- Tilt forward a small amount.
- The wheels should respond in the direction that would move the base under the center of mass (intuitively, trying to “catch” the fall).

**Checkpoint**
- **PASS**: Axis is correct, upright setpoint is clearly defined, and the motor response looks corrective.
- **FAIL**: The response clearly amplifies the tilt—stop immediately and fix sign conventions before tuning.

If you’re unsure whether the response is corrective, reduce output limits further and test with very small tilts. Don’t move on until you are confident the loop direction makes sense.

---

### Step 8 — First closed-loop tests (low-risk)

At this point, you’re not trying to “balance perfectly.” You’re proving the loop is wired correctly and behaves safely.

**Recommended setup**
- Wheels off the ground for the first attempts.
- Conservative output limits.
- Fast power cutoff ready.

**What to watch**
- Small forward tilt → wheels respond to “catch” it.
- Small backward tilt → wheels respond the opposite way.
- No sudden max-power bursts from tiny sensor noise (if you see this, stop and inspect filtering, scaling, and output limits).

**Checkpoint**
- **PASS**: Response is consistently corrective and predictable.
- **FAIL**: Runaway, unpredictable bursts, or direction flips—debug sign/mapping/filtering before PID changes.

---

## PID tuning workflow (practical, repeatable)

Avoid copying gain numbers from other builds. Different IMUs, wheel diameters, gear ratios, motor drivers, batteries, and center-of-mass height can change the needed gains dramatically.

Use a structured method and record each change. If you can log values (angle, target, motor command, encoder speed), even at low rate, it will save time—but don’t assume logging is available.

### 0) Set guardrails before tuning
Before touching gains, make sure you have:
- A known-good upright setpoint.
- Output limits that prevent full-power runaway during early testing.
- A consistent test routine (same floor surface, same battery state as much as possible).

If the robot behaves differently when the battery voltage changes, treat that as normal system variation and tune conservatively.

### 1) Start with the balance loop only (reduce complexity)
If your firmware has multiple layers (angle balance, velocity, position), begin by simplifying:
- Disable or minimize speed/position contributions until basic balance response is correct.
- Focus on the loop that directly stabilizes pitch angle.

**Goal:** controlled “trying to stand” behavior without violent oscillation.

### 2) Tune P first (proportional)
Increase **P** gradually:
- Too low: weak correction; it feels like it “gives up.”
- Too high: rapid oscillation or twitchy behavior.

**Pass condition:** it reacts promptly to small tilts without immediately entering high-frequency oscillation.

### 3) Add D to damp oscillation (derivative)
Add **D** slowly to reduce overshoot:
- Too little D: it overshoots and rings after disturbances.
- Too much D: jitter/noise sensitivity (especially if your angle signal is noisy).

**Pass condition:** it looks calmer near upright and recovers from small taps without ringing.

Practical note: Derivative amplifies noise. If adding D makes it worse, pause and re-check IMU noise, filtering, and scaling rather than forcing D higher.

### 4) Add I only when you need it (integral)
Integral helps with steady bias (slight lean, offset drift), but can create slow instability via wind-up.
- Start very small.
- If your firmware supports anti-windup or integral limits, enable them.
- If it balances briefly then slowly “walks” into a fall, reduce I and re-check your upright reference and mechanical symmetry.

**Pass condition:** it can hold near upright without slowly building an offset that causes a delayed crash.

### 5) Re-introduce encoder-based layers carefully (if used)
Once balance is stable, you can bring in velocity/drive features:
- Add velocity control gradually.
- Confirm that commanding slow forward motion doesn’t immediately destroy balance.
- Keep output limits while validating direction and sign.

A common integration mistake is encoder sign mismatch: “forward command” creates “backward measured speed,” which can destabilize a speed loop. Re-check Step 5 when you add velocity control.

If you want official background on STM32 motor-control ecosystem concepts (without assuming a specific kit firmware), see:
- [ST motor control ecosystem](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

---

## “Ready” milestones

Use these milestones to decide what to work on next.

1) **Bring-up ready**
- Motors respond correctly (mapping + direction).
- Encoders read reliably with consistent sign.
- IMU angle is stable, smooth, and mapped to the correct axis.

2) **Control-ready**
- Closed-loop response is corrective (not runaway).
- With conservative limits, it attempts to stabilize without violent oscillation.

3) **Tuning-ready**
- P and D yield a controlled response near upright.
- I is minimal and doesn’t create delayed instability.
- It can remain near upright for meaningful moments (even if it still needs refinement).

4) **Feature-ready (optional)**
- Encoder-based speed/drive features don’t destabilize balance.
- You can command slow forward/back motion and recover.

---

## Troubleshooting (symptom → likely cause → next action)

**Motors spin but it “runs away” when tilted**
- Likely cause: control sign inverted (angle sign and/or motor direction sign).
- Next action: stop immediately; invert one sign at a time and re-test wheels-off-ground.

**One wheel fights the other**
- Likely cause: left/right motor mapping swapped, or one motor direction inverted.
- Next action: redo Step 4 and redefine “forward” consistently for both wheels.

**Encoder counts don’t change**
- Likely cause: wrong connector/pins, missing wiring, configuration mismatch, or encoder not powered.
- Next action: verify wiring physically, then confirm pin mapping/config; don’t tune PID yet.

**Encoder direction is backwards**
- Likely cause: A/B swapped or sign inversion needed.
- Next action: swap channels (if wiring allows) or invert sign in software; then re-check Step 5.

**IMU angle is noisy/jittery**
- Likely cause: loose IMU mounting, electrical noise, poor filtering, or scaling issues.
- Next action: rigidly mount IMU, verify power stability, reduce D while debugging.

**Oscillates rapidly near upright**
- Likely cause: P too high, D too low, or D amplifying noise.
- Next action: lower P first, then add D gradually; confirm IMU signal quality.

**Balances briefly then slowly falls after a few seconds**
- Likely cause: integral wind-up, drift, or upright reference offset.
- Next action: reduce I, check setpoint, verify mechanical symmetry and sensor offset handling.

**It only works when lifted, but fails immediately on the ground**
- Likely cause: insufficient torque at chosen power level, mechanical friction, or gains not robust under load.
- Next action: check wheel friction and drivetrain alignment; verify power delivery; retune conservatively under real load with output limits.

---

## References

**Internal**
- [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)
- [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)

**Official (STM32 tooling/ecosystem)**
- [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)
- [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- [ST motor control ecosystem](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

---

## FAQ

### Do you provide exact wiring diagrams or firmware files for every kit revision?
This guide is designed to work across revisions and sellers. Use it to validate your specific build step-by-step without assuming a single fixed wiring layout or codebase. If your kit includes a wiring sheet, treat that as the primary reference and use this tutorial as a bring-up checklist.

### What should I verify first if I only have 30 minutes?
Do Step 4 (motor mapping/direction), Step 5 (encoder sanity), and Step 7 (IMU axis/upright reference + control sign sanity). Those three prevent most “instant failure” tuning loops.

### Can I tune PID without encoder feedback?
You can often validate basic balance response without encoders, but encoder feedback is typically important for stable speed/drive behavior. Treat encoder validation as a core bring-up step if you plan to add motion features.

### Why keep recommending “wheels off the ground” early?
It lets you detect mapping and sign mistakes without the robot launching across the room. It’s the safest way to catch runaway behavior before it becomes a hardware problem.

### What does “PASS” mean in this tutorial?
“PASS” means you observed the expected behavior on your own hardware. If your kit behaves differently, treat it as “FAIL” and investigate before moving on.
