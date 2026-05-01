---
status: draft
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: true
publish_target: WordPress
---

# STM32 Self-Balancing Car Kit setup + PID calibration checklist (draft)

## What this tutorial is (and is not)
This is a **review-required** setup checklist for a two-wheel **STM32 self-balancing car kit** that uses an **IMU** for attitude sensing and **encoder motors** for wheel feedback, and may also include **ultrasonic** and **app control** features. Use it to structure your first build and tuning session. You must **verify your kit contents, wiring, firmware, and observed behavior on your own build** before relying on any step.

## Before you start: workspace + tools
- A clear bench area where the robot can safely fall without damaging parts.
- Basic hand tools for the chassis hardware (small screwdrivers, hex driver set, cutters).
- A stable power source appropriate for your kit’s battery holder and wiring (confirm polarity before power-on).
- A way to program your STM32 board (confirm your board’s programming interface on your hardware).
- A method to view debug output (serial/logging) if your firmware supports it.

## 1) Inventory check (do this before assembly)
On the kit page, the “What’s Included” list mentions items such as an **STM32-based robot kit**, a **two-wheel chassis**, an **IMU module**, **encoder gear motors**, an **ultrasonic module**, and **battery holder + wiring**, plus **source code and learning materials**. Confirm what you actually received and set aside anything optional (like ultrasonic) until the core balance loop works.

Checklist:
- Identify the STM32 controller board and verify it powers up without smoke/heat.
- Identify the IMU board and note any axis arrows or orientation markings.
- Identify left/right motors and locate encoder connectors (if separate).
- Identify motor driver hardware (standalone driver or integrated board) and its motor/power terminals.
- Identify any optional add-ons (ultrasonic module, Bluetooth/app-control module) and keep them unplugged for first bring-up.

## 2) Mechanical setup sanity (tighten first, tune later)
Balancing robots are sensitive to looseness. Before wiring:
- Tighten chassis screws, motor mounts, and wheel hubs so nothing wobbles.
- Ensure both wheels spin freely with minimal friction.
- Keep the IMU mounting location rigid; avoid foam tape for first tuning unless the kit explicitly requires it.
- Route cables so they cannot touch the wheels during a fall.

## 3) Wiring checklist (power off while plugging)
Because kit revisions vary, follow your board labels and your documentation. Use this conservative order:

1. **Motors to driver**
   - Connect each motor to the motor driver outputs.
   - Keep left and right consistent with your intended “forward” direction.

2. **Encoders to MCU**
   - Connect encoder channels to the MCU pins expected by your firmware.
   - If connectors are keyed, do not force them.

3. **IMU to MCU**
   - Connect IMU power and bus lines (commonly I²C or SPI, depending on your hardware).
   - Double-check IMU voltage requirements before powering.

4. **Battery/power**
   - Confirm polarity, then connect battery holder wiring to the power input.
   - If there is a power switch, leave it OFF until firmware is ready.

Bring-up rule: if anything gets hot, smells, or resets repeatedly, power off immediately and re-check wiring.

## 4) Firmware bring-up (minimum viable loop)
Your first goal is not “standing balance.” Your first goal is **clean sensor reading + controlled motor output**.

- Flash firmware that can read IMU angle/rate and drive motors with a capped PWM.
- Confirm the IMU is detected and returns changing values when you tilt the robot by hand.
- Confirm each motor spins under command at low speed.
- Verify encoder counts change when you rotate each wheel by hand.

Do not enable full PID balance until these four checks pass.

## 5) IMU orientation + bias checks
Self-balancing control fails quickly if axes are wrong.

Checklist:
- Hold the robot upright and slowly tilt forward/back; confirm the reported “pitch” (or equivalent) changes in the expected direction.
- If the sign is reversed, fix it in firmware (axis mapping or sign flip) rather than “tuning around it.”
- Keep the robot still for a few seconds at boot if your firmware performs gyro bias calibration; verify that behavior in your own code/materials.

## 6) PID calibration workflow (safe, incremental)
Use a staged approach so you can stop safely.

### Stage A: Stabilize angle only
- Start with a very low output limit so the robot cannot launch.
- Increase **P** until it begins to resist falling but does not oscillate rapidly.
- Add a small **D** to reduce overshoot and “buzzing.”
- Keep **I** at zero initially to avoid slow drift runaway.

### Stage B: Add speed/position stabilization (if your firmware supports it)
Many balancing cars layer loops (angle inner loop, speed outer loop) using encoder feedback.
- Confirm encoder direction is correct for both wheels.
- Tune the speed/position loop gently; aggressive outer-loop gains can destabilize an otherwise good angle loop.

### Stage C: Add integral cautiously
- Add small **I** only after the robot can balance briefly with P and D.
- Watch for slow-growing oscillation or motor heating; if seen, reduce I and verify bias/leveling.

## 7) Optional modules (only after balance works)
If your kit supports **ultrasonic obstacle avoidance/following** or **app control**, integrate one feature at a time:
- Wire the module, confirm it is detected, and confirm its data is reasonable.
- Do not change core PID gains while adding new features unless you can reproduce issues reliably.

## Related pages (for review)
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials index: https://feigen8n.online/tutorials/
