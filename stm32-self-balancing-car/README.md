# STM32 Self-Balancing Car Kit — Setup & PID Calibration Checklist (Draft)

This repository provides a **verify-on-your-build** workflow for bringing up a **typical two-wheel self-balancing robot car** (often STM32-based), validating sensor/motor directions, and tuning PID gains safely. Kit revisions vary—do not assume specific modules, firmware, or results.

## Validation Status (as of 2026-04-30)
- This README is a **draft for human review**.
- Steps below are **checklists** to validate on your own hardware.
- No kit-contents, firmware-availability, or performance claims are made.

## Verify your kit (before assembly)
Use the product/kit page “What’s Included” section and/or your packing list to confirm what you actually have. Common categories to identify:
- Controller board + programming interface (varies by revision)
- Motors + motor driver stage
- Attitude sensor module (if your build uses one; often an IMU)
- Wheel feedback (encoders, if present)
- Power parts (battery holder/wiring/switches)

## Safety & Bench Setup
- Use a clear bench; support the chassis so wheels can spin freely during first power-on.
- Verify polarity, confirm no shorts, and keep a power-off path reachable.
- Keep hands, hair, and loose cables away from spinning wheels.

## Bring-Up Checklist (No PID Yet)
1. Visual inspection: connectors seated, no pin misalignment.
2. Power sanity: controller stays on without heating/resets.
3. Sensor sanity (if used): readings change plausibly when tilting by hand.
4. Motor sanity: each motor spins slowly on command (wheels off ground).
5. Encoder sanity (if present): counts change when rotating wheels by hand.
6. Sign mapping: confirm “forward” motor direction and encoder sign match your firmware assumptions.

Stop and fix any failure before attempting balance control.

## Sensor Orientation & Bias Notes
- Confirm sensor axes/sign match the physical mounting on your chassis.
- If your firmware does a still-at-boot bias step, keep the robot still and verify it completes (by logs/behavior).
- Do not “tune around” a reversed axis—fix mapping/sign first.

## First Balance Attempts (Conservative)
- Limit motor output; use a soft start.
- Increase gains slowly; prioritize controllability over “standing up”.
- If it accelerates into the fall, re-check axis sign and motor direction before changing gains.

## PID Tuning Workflow (Practical Order)
1. Stabilize sensor math (no rapid drift while held still).
2. Tune **P** until it resists falling; back off if it oscillates.
3. Add **D** to reduce overshoot and fast wobble (watch for noise sensitivity).
4. Add small **I** only after brief stable balance is possible; watch for wind-up.
5. If using an outer speed loop, tune it gently after the inner angle loop is stable.

Record gains and test conditions (surface, battery state, wheel traction) for repeatability.

## Optional Modules (Only if your kit includes them)
- Wireless/app control: validate command latency; set safe limits.
- Distance/obstacle sensing: validate mounting and range; integrate without destabilizing the balance loop.

## Troubleshooting Checklist
- Violent oscillation: reduce P, add D, check sensor noise/mounting.
- Slow drifting tip: re-check bias/calibration; only then consider small I.
- Wheels fight each other: re-check motor direction and encoder sign per wheel.
- Random resets: re-check power wiring and current capability on your build.

## Optional documentation media (add your own)
If you want to document your build, create files like:
- `docs/media/bench-power-on.mp4`
- `docs/media/encoder-check.mp4`
- `docs/media/first-balance-attempt.mp4`

## Related
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial slug (draft target): `/tutorials/stm32-self-balancing-car-setup/`
