---
status: publish
date: 2026-04-30
project: stm32-self-balancing-car-kit
slug: stm32-self-balancing-car-setup
review_required: false
publish_target: WordPress
---

# STM32 self-balancing car setup and PID calibration checklist

This is a practical, step-by-step checklist to bring up a two-wheel STM32 self-balancing car build safely and reach a point where you can tune balance control. Kit contents, wiring, and firmware steps vary by seller and revision—treat each step as “passed” only after you confirm it on your own hardware.

Related pages:
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials hub: https://feigen8n.online/tutorials/

## Before you start (safety + expectations)
- Work on a clear bench; plan a quick power-off (unplug battery first).
- Keep the robot lifted (wheels off the table) for initial sensor and motor checks.
- Do not assume motor direction, IMU orientation, or encoder polarity—verify each one.
- Avoid prolonged high-power free-spinning tests; some motors/drivers can overheat.

## Confirm what you actually have (identify your modules)
Use board markings and your seller listing to identify what’s on your build:
- Controller board and power input connector/range (from silkscreen or listing notes).
- IMU board/interface (I2C vs SPI), pinout, and expected logic level.
- Motors and encoder wiring (A/B channels, power/ground, connector style).
- Any optional control add-ons (for example, “app control” may require a separate module).
- Any optional sensors your listing mentions (for example, a distance sensor): only wire and enable if your kit actually includes it and you can confirm pin/voltage requirements.

## Mechanical assembly checks
- Tighten chassis hardware; confirm wheels spin freely without rubbing.
- Mount the IMU rigidly (minimize vibration and flex).
- If IMU axis orientation is unknown, plan to verify axis/sign during the sensor test.

## Wiring checklist (verify against board labels)
- Power: confirm polarity before connecting; route wires to avoid strain on connectors.
- Motors: connect left/right outputs; don’t worry about direction yet.
- Encoders: connect power/ground and A/B signals to the intended pins; label A/B.
- IMU: connect SDA/SCL (or SPI), power, and ground; confirm voltage compatibility.
- Optional modules (only if present on your build): wire per their own pinout, and keep them disabled in firmware until balance is stable.

## Firmware bring-up (minimum viable checks)
- Use your STM32 flashing workflow to program firmware (your own firmware or the one provided with your kit, if any).
- If available, start in a “safe/test mode” with motors disabled so you can validate sensors first.
- Confirm the control loop timing is fixed and repeatable (timer-driven is typical); unstable timing makes tuning unreliable.

## Sensor sanity checks (must pass before PID tuning)
With the robot held still:
- IMU angle/sign: gently tip forward/back; confirm the reported direction matches reality.
- Gyro sign: rotate the chassis; confirm rate sign matches the rotation direction.
- Encoders: rotate each wheel by hand; confirm counts change smoothly and left/right aren’t swapped.
If any sign is inverted, fix it now (swap wires, swap A/B, invert in software), then re-check.

## PID calibration checklist (balance first)
1. Disable extras: keep optional modules and remote/app commands out of the loop until balance is repeatable.
2. Add conservative motor limits: clamp output so early tuning can’t drive extreme power.
3. Tune P first: increase gradually until it resists falling; back off if oscillation is harsh.
4. Add D for damping: increase slowly to reduce wobble/overshoot; reduce if noise makes it twitchy.
5. Add I last (only if needed): use small I for slow bias; add anti-windup to avoid runaway after saturation.
6. Re-check direction: if it accelerates the fall, a sign convention is wrong—stop and fix.
7. Progress in stages: wheels-in-air → on-ground with support → short free-standing attempts.

## Troubleshooting (symptom → likely cause)
- Immediate runaway: feedback sign wrong (angle, motor direction, or mixing).
- High-frequency shaking: P too high, D too high, noisy IMU, or loose IMU mount.
- Slow drift then sudden lurch: integral windup or output saturation without anti-windup.
- Works lifted, fails on floor: insufficient torque, wrong center of mass, or encoder terms misconfigured.

## Next steps
After upright balance is repeatable, re-enable optional features one at a time (encoder speed control, app control, optional sensors) and re-check stability after each change. When documenting your build, phrase features as “confirmed on my unit” and avoid assuming exact kit contents.
