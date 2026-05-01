# STM32 Self-Balancing Car Kit — Setup & PID Calibration Checklist (Draft)

This repository documents a **two-wheel STM32-based self-balancing robot car kit** that uses an **IMU attitude sensing module** and **encoder gear motors** for balance control, with optional **app control** and an **ultrasonic module** for basic obstacle behaviors. The goal is a repeatable, verify-on-your-build workflow for bringing up the hardware, confirming sensor directions, and tuning PID gains safely.

## Validation Status (as of 2026-04-30)

- This README is a **draft for human review**.
- All procedures below are **checklists** intended to be verified on your own build.
- No hardware performance claims are made here, and no results are implied without your measurements.

## What’s Included (Kit Facts)

- STM32-based self-balancing robot car kit  
- Two-wheel balancing chassis  
- IMU attitude sensing module  
- Encoder gear motors  
- Ultrasonic module  
- Battery holder and wiring  
- Source code and learning materials  

## Safety & Bench Setup

- Test on a **clear bench** with the robot supported so wheels can spin freely during first power-on.
- Keep hands, hair, and loose cables away from spinning wheels.
- Start with **low supply risk**: verify polarity, confirm no shorts, and only then connect the battery holder.

## Bring-Up Checklist (No PID Yet)

1. **Visual inspection**: Confirm connectors are fully seated and there is no pin misalignment.
2. **Power sanity**: Power on and confirm the controller stays on without resets or heating.
3. **IMU presence**: Verify the firmware detects the IMU and streams plausible raw readings.
4. **Encoder presence**: Verify both wheel encoders produce counts when wheels are rotated by hand.
5. **Motor direction mapping**: Command each motor slowly and confirm “forward” in firmware matches physical forward.
6. **Encoder sign mapping**: Confirm encoder count increases in the expected direction for each wheel.

If any item above fails, stop and fix it before attempting balance control.

## IMU Orientation & Calibration Notes

- Confirm the firmware’s assumed **IMU axes** match the IMU’s physical mounting on your chassis.
- Perform an IMU **offset calibration** with the robot held still, and record the resulting offsets in your configuration.
- Verify that the “tilt forward/back” reported by your attitude estimator changes in the correct direction when you tilt the chassis by hand.

## First Balance Attempts (Conservative)

- Use a **soft start** and limit motor output during initial tuning so the robot does not launch off the bench.
- Verify that the control loop frequency and sensor update rate are stable on your setup before increasing gains.

## PID Tuning Workflow (Practical Order)

1. **Stabilize sensor math**: Confirm the estimated tilt is not drifting rapidly when the robot is held still.
2. **Tune balance P**: Increase proportional gain gradually until the robot begins to resist falling, then back off to reduce oscillation.
3. **Add D for damping**: Increase derivative gain to reduce overshoot and fast wobble, then re-check that noise does not dominate.
4. **Add small I only if needed**: Introduce integral gain carefully to correct steady bias, and verify it does not cause slow “wind-up” tipping.
5. **Re-check signs**: If the robot accelerates into the fall, re-check IMU axis sign, motor direction, and encoder sign before changing gains further.
6. **Confirm repeatability**: Power-cycle and re-test to ensure the behavior is consistent across restarts.

Record your final gains and the test conditions (surface, battery state, wheel traction) because these affect results.

## Optional Modules (Verify on Your Build)

- **App control support**: Validate command latency and define safe limits for manual driving while balancing.
- **Ultrasonic obstacle behavior**: Validate sensor mounting angle and minimum range, then confirm any avoidance/following behavior does not destabilize balance.

## Troubleshooting Checklist

- **Violent oscillation**: Reduce P, add D, and confirm IMU noise is not excessive.
- **Slow drifting tip**: Re-run IMU offset calibration; only then consider small I.
- **One wheel fights the other**: Re-check motor direction and encoder sign per wheel.
- **Random resets**: Re-check power wiring, connector seating, and current limits for your motor drive stage.

## Demo Media Placeholders

Add your own verified media to document your build:

- `docs/media/bench-power-on.mp4` — first power-on with wheels off the ground  
- `docs/media/encoder-check.mp4` — hand-rotation count direction proof  
- `docs/media/first-balance-attempt.mp4` — conservative gains on a safe surface  
- `docs/media/app-control-demo.mp4` — optional, only if your setup supports it  
- `docs/media/ultrasonic-demo.mp4` — optional, only if installed and validated  

## Related

- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/  
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/  
- Tutorials hub: https://feigen8n.online/tutorials/  
- Planned tutorial slug (draft target): `/tutorials/stm32-self-balancing-car-setup/`
