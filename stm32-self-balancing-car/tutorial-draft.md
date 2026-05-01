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
This is a **review-required** setup and tuning checklist for a **typical two-wheel STM32 self-balancing car** workflow. Kit revisions vary, so treat this as a **structure for verification**—not a promise of included parts, firmware, or results. If your kit includes optional modules (for example, distance sensing or wireless control), validate the core balance loop first, then add features one at a time.

## Before you start: workspace + tools
- Clear bench area where the robot can safely fall without damaging parts.
- Basic hand tools for chassis hardware (small screwdrivers, hex drivers, cutters).
- Power source appropriate for **your** battery holder/wiring (confirm polarity before power-on).
- A way to program **your** controller (confirm SWD/USB-UART/boot mode for your board).
- A way to observe behavior safely (wheel-off-ground support; optional serial/logging if your firmware provides it).

## 1) Inventory check (do this before assembly)
Check the kit/product page **“What’s Included”** section (or your packing list) and confirm what you actually received. Do not assume any module is included unless you can identify it in-hand.

Checklist:
- Identify the controller board (STM32-based or similar) and confirm basic power/connector condition.
- Identify motor + driver parts (and any separate encoders, if present on your motors).
- Identify the attitude sensor module (often an IMU) **if your kit uses one**, and note orientation markings.
- Identify power parts (battery holder, switch, wiring harnesses) and inspect for damage.
- Set aside any optional add-ons until core bring-up is stable.

## 2) Mechanical setup sanity (tighten first, tune later)
- Tighten chassis screws, motor mounts, and wheel hubs so nothing wobbles.
- Ensure both wheels spin freely with minimal friction.
- Mount the attitude sensor rigidly; avoid “soft” mounting unless your documentation explicitly calls for it.
- Route cables so they cannot touch wheels during a fall.

## 3) Wiring checklist (power off while plugging)
Because pinouts and revisions vary, follow **your board labels** and **your documentation**.

Conservative order:
1. Motors → driver outputs (keep left/right consistent).
2. Encoders → MCU inputs (if your motors have encoders; don’t force keyed plugs).
3. Sensor module → MCU bus (I²C/SPI/UART depending on your hardware; verify voltage levels).
4. Battery/power wiring → power input (confirm polarity; leave switch OFF until firmware is ready).

Bring-up rule: if anything heats, smells, browns out, or resets repeatedly, power off and re-check wiring.

## 4) Firmware bring-up (minimum viable loop)
Goal: **clean sensor reading + controlled motor output**, not instant balancing.

Checklist:
- Use firmware you trust (vendor, community, or your own) that can (a) read the attitude sensor (if used) and (b) command motors with a safe output cap.
- Confirm sensor values change plausibly when you tilt the chassis by hand (if applicable).
- Confirm each motor can spin slowly on command (wheels off the ground).
- Confirm encoder counts change when you rotate wheels by hand (if encoders are part of your build).

Do not enable full PID balance until these checks pass.

## 5) Sensor orientation + bias checks
- Tilt forward/back slowly; confirm the reported pitch/angle signal changes in the expected direction.
- If the sign is reversed, fix axis mapping/sign in firmware rather than “tuning around it.”
- If your firmware performs a still-at-boot bias step, keep the robot still and confirm (by logs/behavior) that calibration actually completes on your build.

## 6) PID calibration workflow (safe, incremental)
### Stage A: Stabilize angle only
- Start with a low output limit.
- Increase **P** until it resists falling; back off if it chatters/oscillates.
- Add a small **D** to reduce overshoot and fast wobble.
- Keep **I** at zero initially.

### Stage B: Add speed/position stabilization (only if your firmware uses encoders)
- Confirm encoder direction/sign is correct per wheel.
- Tune the outer loop gently; aggressive outer gains can destabilize the inner loop.

### Stage C: Add integral cautiously
- Add small **I** only after brief stable balance is possible.
- Watch for slow-growing oscillation, drift, or motor heating; if seen, reduce I and re-check bias/leveling.

## 7) Optional modules (only after balance works)
If your build includes optional modules (distance sensor, wireless/app control, etc.):
- Integrate one feature at a time and validate its readings/latency first.
- Avoid changing core PID gains while adding new features unless you can reproduce issues reliably.

## Related pages (for review)
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials index: https://feigen8n.online/tutorials/
