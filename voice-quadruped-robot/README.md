# Voice Quadruped Robot — Assembly & First Movement Checks (check-your-kit)

This repository provides a checklist-style guide for assembling a DIY voice-controlled quadruped robot kit and running safe first movement checks on your specific kit revision. It focuses on observable validation (alignment, symmetry, range-of-motion, and safe power-on behavior) without assuming exact board, firmware, or included resources.

## Scope and boundaries

- **Covered:** Mechanical assembly checks, wiring sanity checks, first power-on safety posture, basic motion checks (e.g., short forward/back checks if your kit’s demo supports them), and a voice interaction test plan.
- **Not claimed:** Exact pinout/port map, exact firmware setup steps, guaranteed behavior across revisions, or any measured performance outcomes.
- **Kit contents:** Refer to the kit/product page and your in-box packing list; verify what you received before starting.

## Safety and power notes

- Treat first power-on as a motion hazard; keep the robot lifted so legs can move freely.
- Do not force joints; if anything binds, power off and fix alignment before trying again.
- If you observe resets, strong twitching, continuous buzzing, or repeated clicking, stop and re-check connectors, power stability, and mechanical friction.

## Tools and prep (validate your kit)

- A clean work surface and small hand tools appropriate for your kit hardware.
- A stable power method as described by your kit’s included instructions.
- Access to whatever “assembly/demo resources” shipped with your kit revision.

## Assembly checklist (mechanical-first)

1. Inventory: confirm key part categories and any included reference materials.
2. Frame alignment: chassis sits square on a flat surface (unpowered).
3. Leg symmetry: left/right legs are mirrored correctly before final tightening.
4. Servo seating: servos are secured and cannot rotate in their mounts.
5. Cable routing: wires have slack and cannot snag on moving joints.
6. Fastener re-check: re-check after the first short motion check.

## Bring-up: first power-on (movement-safe)

1. Lift the robot (feet off the table).
2. Apply power and watch for binding, grinding, or a joint driving to an extreme.
3. If a neutral/idle mode exists for your revision, enter it before attempting motion.
4. If motion is asymmetric, power off and re-check that leg’s assembly, connector seating, and mapping.

## Motion checks (use your included demo/modes)

- Idle/neutral: stable posture without escalating buzzing.
- Single action: one simple movement supported by your resources; stop on dragging/tipping.
- Short forward/back: look for strong yaw/drift and obvious asymmetry.
- Demo/motion mode (if available): run briefly first; stop if binding appears near end-of-travel.

## Voice interaction test plan (varies by revision)

1. Start in a stable stance or lifted position.
2. Enable voice mode using your kit’s included instructions/resources.
3. Test a small set of commands supported by your revision and record what happens.
4. If voice triggers movement, repeat only on a clear surface and be ready to cut power.

## Troubleshooting quick checks

- Turns instead of walking straight: verify mirrored assembly and cable freedom.
- One leg jitters/stalls: re-seat connectors; confirm free motion by hand when unpowered.
- Hops/scrapes: verify linkage angles and body/leg clearance.
- Works once then degrades: re-check fasteners and cable tension near end-of-travel.

## Related

- Tutorials hub: https://feigen8n.online/tutorials/
- Kit page: https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/
- Product page: https://feigen8n.online/product/diy-voice-quadruped-robot-kit/
