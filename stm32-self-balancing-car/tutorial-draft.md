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

A two-wheel self-balancing robot is one of the fastest ways to *feel* control theory become real: it either stands up, oscillates, or face-plants. This tutorial is a practical setup and PID calibration checklist for a typical **STM32 self-balancing car kit** with an **IMU** for attitude sensing and **encoder motors** for feedback. It is written for builders who want a safe, repeatable bring-up process and clear “pass/fail” checkpoints before they spend hours tuning.

This is **not** a promise of exact steps for one fixed kit revision. Kit contents, wiring, and firmware steps vary by seller and revision—treat each step as “passed” only after you confirm it on your own hardware.

**Related pages**
- Kit page: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- Product page: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)
- Tutorials hub: [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)

---

## Who this is for (and what problem it solves)

**You’ll benefit most if you:**
- Have an STM32-based balancing car kit (or plan to buy one) and want a realistic setup plan.
- Want to avoid guessing: you prefer checkpoints like “IMU orientation makes sense” and “motors spin the correct direction” before tuning.
- Need a PID workflow that starts with safety, then progresses from “moves” to “balances”.

**This checklist helps solve:**
- “It powers on but does nothing” (bring-up gaps).
- “Motors fight each other / wrong direction” (sign conventions and wiring).
- “It oscillates like crazy” (PID gains too aggressive or incorrect loop wiring).
- “It falls immediately” (IMU axis mapping/offset, wrong upright reference, or control sign errors).

---

## Before buying: what to verify (so your setup is smoother)

If you’re still shopping, validate these basics early using the kit listing and any included docs you receive. The [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/) is positioned for hands-on learning around **PID control**, **IMU attitude sensing**, **encoder motor feedback**, and potentially **app control**—but implementations vary.

**Checklist to confirm before you commit time:**
1. **Controller family is STM32** (exact model can vary; don’t assume pinouts).
2. **IMU presence and mounting**: the board/module is physically mounted rigidly (wobble = noise).
3. **Motor + encoder feedback**: encoder wiring exists and can be connected cleanly.
4. **Power path clarity**: you know what powers logic vs motors, and where ground is shared.
5. **A path to build/flash firmware**: you have a development workflow you can use (commonly via STM32 tooling).

If you already bought the kit, keep reading—this guide is structured so you can progress even when details differ.

---

## Safety first: power and mechanical checks (do these before firmware)

Balancing robots can unexpectedly lurch. Your goal is to reduce risk *before* a control loop can command full power.

**Mechanical “no-power” checks (PASS/FAIL):**
- **PASS**: Wheels spin freely by hand with minimal rubbing.
- **PASS**: Chassis is symmetric (left/right wheel alignment similar).
- **PASS**: IMU module is firmly fixed; no loose standoffs that let it vibrate.
- **PASS**: Nothing can short the underside of boards against metal fasteners.
- **FAIL**: Wheel binds, IMU is floating, or wires can hit wheels. Fix first.

**Power safety setup:**
- Keep the robot **off the ground** for the first motor tests (a small box stand works).
- Start with **limited power** where possible (lower-voltage source or current-limited supply if you have one).
- Prepare an emergency cutoff: unplugging or a switch you can reach quickly.

---

## Setup workflow (step-by-step) with validation checkpoints

Use this workflow in order. Each step ends with a checkpoint you can evaluate on your hardware.

### Step 1 — Document your kit revision (10 minutes)

Because kit revisions vary, spend a few minutes creating your own “map”:
- Take photos of wiring and connectors.
- Note any labels on boards and IMU module orientation (which edge faces forward).
- Identify: motor connectors, encoder connectors, power input, and any programming/debug header.

**Checkpoint**
- **PASS**: You can point to each connector and describe what it likely does (motor, encoder, power, programming).

---

### Step 2 — Establish a firmware build/flash path (without assuming code)

Your next bottleneck is usually “can I build and flash something reliably?”. If you use ST’s toolchain, start here:
- [STM32CubeIDE documentation](https://www.st.com/en/development-tools/stm32cubeide.html)

If your kit provides an alternate workflow, that’s fine—use what matches your hardware.

**Checkpoint**
- **PASS**: You can flash *something* to the board (even a minimal test) and repeat it reliably.
- **FAIL**: Flashing is intermittent or unclear—don’t attempt PID tuning until flashing is stable.

---

### Step 3 — Verify power rails and ground (logic vs motors)

Balancing robots are sensitive to brownouts and noise. Before running control code:
- Confirm the logic side powers consistently.
- Confirm motors have a suitable supply and share a proper ground reference with the controller (unless the design explicitly isolates it).

**Checkpoint**
- **PASS**: The board powers on consistently with no resets when you gently wiggle the power connector.
- **FAIL**: Random resets or power flicker—fix power wiring/connector seating before motor tests.

---

### Step 4 — Motor direction test (open-loop, no balancing yet)

This is the most important “sign convention” test. Your kit may have app control; regardless, you need a way to command each motor forward/backward at low duty.

Test sequence:
1. Lift the robot so wheels are free.
2. Command **left motor** slowly forward, then reverse.
3. Command **right motor** slowly forward, then reverse.
4. Define what “forward” means for your build (e.g., robot would roll forward on the floor).

**What you’re checking**
- Each motor spins reliably.
- Left/right mapping is correct.
- “Forward” commands actually correspond to forward wheel motion.

**Checkpoint**
- **PASS**: Left command affects left wheel, right affects right wheel, and forward/reverse are consistent.
- **FAIL**: Swapped motors, inverted direction, or intermittent rotation—fix wiring or software mapping now.

---

### Step 5 — Encoder sanity check (counts move the right way)

Encoder feedback is essential for stable speed/position control layers (often nested under balance).

Test idea (hardware-agnostic):
- Rotate a wheel forward by hand and observe the encoder count change.
- Rotate backward and confirm the count changes in the opposite direction.
- Repeat for both wheels.

**Common pitfalls**
- Counts don’t change: wrong connector, missing pullups, incorrect pin mapping, or dead encoder wiring.
- Counts change but direction is inverted: A/B channels swapped or sign inversion in software.

**Checkpoint**
- **PASS**: Both encoders change consistently with wheel motion and the direction sign makes sense.
- **FAIL**: No counts or nonsense values—do not tune PID until encoder readings are trustworthy.

---

### Step 6 — IMU “stillness” check (noise and offsets)

The IMU is the balancing robot’s sense of “upright.” Before you care about perfect calibration, confirm basic sanity:
- With the robot stationary, IMU readings should be relatively stable (not jumping wildly).
- If you tilt the robot forward/backward slowly, the reported tilt should change smoothly in the correct direction.

Because different kits use different IMUs and filtering approaches, focus on these universal observations:
- Smooth response to tilt.
- Consistent sign: forward tilt should consistently increase or decrease the same way each time.
- Repeatability: returning to the same physical position should yield similar readings.

**Checkpoint**
- **PASS**: Tilting the chassis produces a smooth, repeatable change; stationary readings aren’t chaotic.
- **FAIL**: Readings are extremely noisy or reversed unpredictably—check mounting rigidity and configuration.

---

### Step 7 — Confirm “upright reference” and axis mapping (the make-or-break step)

Most “it falls instantly” issues are caused by one of:
- The controller thinks “upright” is a different physical angle.
- Pitch axis is not the axis you’re controlling.
- Control sign is inverted (it pushes the robot further away from upright).

Procedure:
1. Place the robot in the intended upright balancing pose (often near vertical).
2. Observe your “angle” signal.
3. Tilt forward slightly and verify the angle changes in the expected direction.
4. Tilt backward slightly and verify it changes in the opposite direction.

**Checkpoint**
- **PASS**: The angle signal corresponds to the real pitch of the robot, and the “upright” setpoint is clearly defined.
- **FAIL**: Pitch/roll confusion or unclear setpoint—fix this before any PID changes.

---

### Step 8 — First closed-loop attempt: minimize risk

Now you are ready for a careful first try—still *not* for “perfect balance,” but to confirm the loop is wired correctly.

Safety setup:
- Wheels off the ground.
- Limit command output if your firmware supports it.
- Be ready to cut power immediately.

What to watch:
- When you tilt the robot forward slightly, the wheels should respond in the direction that would drive the base under the center of mass (intuitively “catching” the fall).
- If it clearly “runs away” (accelerates in the wrong direction), **stop immediately**: your control sign is likely inverted.

**Checkpoint**
- **PASS**: Response direction looks corrective (it tries to catch).
- **FAIL**: Response is destabilizing (it amplifies the tilt). Do not proceed to tuning.

---

## PID tuning workflow (practical checklist, not magic numbers)

Because hardware and firmware differ, avoid copying gain values from other builds. Use a structured method and record changes.

### 1) Start with the balance loop only (keep it simple)
If your firmware has multiple loops (balance angle, velocity, position), begin by isolating balance behavior:
- Disable or reduce speed/position contributions until basic balance response is correct.
- Focus on the loop that controls angle/pitch.

**Goal:** a controlled “trying to stand up” behavior without violent oscillation.

### 2) Tune P first (proportional)
Increase **P** gradually:
- Too low: it feels weak; it doesn’t try to correct quickly.
- Too high: it oscillates rapidly or becomes twitchy.

**Pass condition:** it responds promptly to small tilts without immediate high-frequency oscillation.

### 3) Add D to damp oscillation (derivative)
Add **D** slowly to reduce overshoot and oscillation:
- Too little D: bounce/overshoot persists.
- Too much D: it becomes noisy or jittery (especially if IMU signal is noisy).

**Pass condition:** it looks “calmer” around upright and doesn’t ring after small disturbances.

### 4) Add I only when you need it (integral)
Integral can help correct steady-state bias (e.g., slight lean). It can also cause slow “wind-up” instability.
- Start very small.
- Use anti-windup if available.
- If it slowly drifts into a fall after a few seconds, reduce I.

**Pass condition:** it can hold near-upright without slowly building an offset that causes a delayed crash.

### 5) Re-enable speed/encoder-based layers carefully
If your kit uses encoder feedback for motion control, bring it back after balance is stable:
- Add velocity control gradually.
- Confirm that commanding forward motion doesn’t destroy balance immediately.
- Keep outputs limited while verifying.

If you want more background on motor control topics within the STM32 ecosystem, see:
- [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

---

## Validation checkpoints (what “ready” looks like)

Use these as milestones. Don’t chase the final one until the earlier ones are solid.

1. **Bring-up ready**
   - Motors respond correctly (direction and mapping).
   - Encoders read reliably.
   - IMU signals are stable and mapped to the correct axis.

2. **Control-ready**
   - Closed-loop response is corrective (not runaway).
   - It can attempt to stand without violent oscillation (even if it can’t fully balance yet).

3. **Tuning-ready**
   - P and D produce a controlled response.
   - I is minimal and doesn’t create delayed instability.
   - It can remain near upright for meaningful moments without drifting into failure.

---

## Troubleshooting (symptom → likely cause → next action)

**Symptom: motors spin but robot “runs away” when tilted**
- Likely cause: control sign inverted (angle sign or motor sign).
- Next action: invert the relevant sign (angle or motor direction) and re-test *wheels-off-ground*.

**Symptom: one wheel fights the other**
- Likely cause: left/right motor mapping swapped or one motor direction inverted.
- Next action: redo Step 4 and ensure “forward” is consistent for both wheels.

**Symptom: encoder counts don’t change**
- Likely cause: wrong connector/pins, missing wiring, or configuration mismatch.
- Next action: verify encoder wiring physically, then confirm software pin mapping.

**Symptom: IMU angle is noisy/jittery**
- Likely cause: loose IMU mounting or noisy power.
- Next action: rigidly mount IMU, check power stability, and reduce derivative (D) while debugging.

**Symptom: it oscillates rapidly near upright**
- Likely cause: P too high or D too low (or IMU noise feeding D).
- Next action: reduce P, then add D gradually; ensure IMU signal is reasonable.

**Symptom: it balances briefly then slowly falls after a few seconds**
- Likely cause: integral wind-up or incorrect offset handling.
- Next action: reduce I, confirm upright reference, and look for bias sources (mechanical imbalance, drift).

---

## Internal links you can use while building

- If you want more project guides, browse the hub: [Tutorials – ESP32 AI Lab](https://feigen8n.online/tutorials/)
- If you’re confirming what the kit is intended to teach (PID + IMU + encoders), start here: [STM32 Self-Balancing Car Kit](https://feigen8n.online/kits/stm32-self-balancing-car-kit/)
- If you’re ready to order or compare purchase options, use: [STM32 Self-Balancing Car Kit (Product)](https://feigen8n.online/product/stm32-self-balancing-car-kit/)

---

## Official external references (tooling and ecosystem)

- [STM32CubeIDE documentation](https://www.st.com/en/development-tools/stm32cubeide.html)
- [ST motor control resources](https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html)

---

## FAQ

### Do you provide exact wiring diagrams or firmware files for this kit?
This checklist is designed to work across kit revisions and sellers. Use it to validate your specific build step-by-step, without assuming a single fixed wiring layout or codebase.

### What should I verify first if I only have 30 minutes?
Do Step 4 (motor direction mapping), Step 5 (encoder sanity), and Step 7 (IMU axis/upright reference). Those three prevent most “instant failure” tuning loops.

### Can I tune PID without encoder feedback?
You can often verify basic balance response without encoders, but encoder feedback is typically important for stable motion control and speed-related behavior. Treat encoder validation as a core bring-up step.

### Why is “wheels off the ground” recommended early?
It lets you verify sign conventions and loop direction without the robot launching itself across the room. It’s a safer way to detect runaway behavior.

### What does “pass” mean in this guide?
“Pass” means you observed the expected behavior on your own hardware, not that a step is theoretically correct. If your kit behaves differently, treat it as “fail” and investigate before moving on.
