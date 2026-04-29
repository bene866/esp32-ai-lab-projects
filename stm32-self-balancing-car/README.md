# STM32 Self-Balancing Car

Setup and calibration notes for an STM32 two-wheel self-balancing car kit with IMU sensing, encoder motor feedback, and PID control learning.

## Overview
This project documents the review path for a self-balancing car demo. The priority is to explain hardware, calibration, and validation status clearly before publishing detailed code or tuning advice.

## Features
- STM32-based two-wheel balancing robot
- PID control learning workflow
- IMU attitude sensing notes
- Encoder motor feedback notes
- App control and ultrasonic function checks after validation

## Hardware List
- STM32 self-balancing robot car kit
- Two-wheel chassis
- IMU module
- Encoder gear motors
- Ultrasonic module
- Battery holder and wiring

## Quick Start
1. Confirm the board and firmware version.
2. Assemble the chassis and motor wiring.
3. Verify IMU orientation.
4. Run a static sensor test.
5. Begin PID tuning only after the sensor readings are stable.

## Demo Media
- Images: `media/`
- Video: add reviewed balance test media after verification.

## Build Notes
- PID values should be marked as starting points, not universal settings.
- Battery and floor conditions affect behavior.
- Document failed calibration cases in troubleshooting.

## Related
- Tutorial draft: https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- Product: https://feigen8n.online/kits/stm32-self-balancing-car-kit/

