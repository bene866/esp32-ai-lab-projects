# Voice Quadruped Robot — Assembly & Movement Test (Verify-on-Your-Build)

This repository is a **verify-on-your-build** guide for assembling a DIY **voice-controlled quadruped robot kit** and confirming basic motion reliably on your specific kit revision. It focuses on repeatable checks you can observe (alignment, symmetry, range-of-motion, and stable power behavior) without assuming exact board/firmware versions.

## Validation status

- **Documentation status:** Draft checklist for human review (2026-05-01).
- **Hardware validation:** Not verified by this repository alone; you must confirm behavior on your build.
- **What is covered:** Mechanical assembly checks, first power-on safety, basic walking (forward/back), and dance/motion demo validation; voice interaction test planning.
- **What is not claimed:** Exact wiring pinout, exact firmware steps, or guaranteed compatibility across revisions.

## Kit scope (from the kit description)

This kit is described as including:
- Quadruped robot body parts
- Servo-driven leg mechanism
- Controller board
- Connection wires
- Assembly and demo resources

Key functions described for the kit:
- Four-legged walking robot design
- Basic forward and backward movement
- Dance and motion demo modes
- Voice interaction support
- DIY assembly experience

## Safety and power notes

- Treat the first power-on as a **motion hazard**. Keep the robot lifted so legs can move without contacting the table.
- Avoid forcing joints. If a leg binds, power off and fix alignment before trying again.
- If you observe repeated resets, twitching, or uneven movement, stop and re-check connectors and mechanical friction before continuing.

## Tools and prep (verify on your build)

- A clean work surface and small hand tools appropriate for your kit hardware.
- A method to provide stable power to the controller board and servos **as your kit documentation specifies**.
- A way to access the kit’s included **assembly and demo resources** so you can trigger movement and voice modes supported by your version.

## Assembly checklist (mechanical-first)

1. **Inventory pass:** Confirm you have body parts, leg mechanism parts, the controller board, and connection wires before starting assembly.
2. **Frame alignment:** Assemble the main body so the chassis is square and not twisted when placed on a flat surface.
3. **Leg symmetry:** Build legs in mirrored pairs and verify left/right parts match orientation before tightening hardware.
4. **Servo seating:** Ensure each servo is fully seated and secured so it cannot rotate within its mount under load.
5. **Cable routing:** Route wires so they do not rub against moving joints and do not pull tight at full leg travel.
6. **Fastener check:** Tighten fasteners to “secure but not crushing,” and re-check after the first short movement test.

## Bring-up: first power-on (movement-safe)

1. Place the robot on a stand so **all feet are off the table**.
2. Apply power and observe the legs for any immediate binding, grinding, or a single joint trying to move beyond its range.
3. If the kit provides a neutral/idle state, enter it before attempting any walking action.
4. If any leg moves asymmetrically, power off and inspect that leg’s assembly for reversed linkages or obstructed joints.

## Movement validation (basic walking + demo modes)

Use your kit’s controller modes/resources to run the following checks:

- **Forward test:** Confirm all four legs contribute to forward motion and that the body does not yaw sharply to one side.
- **Backward test:** Confirm reverse movement is stable and does not cause the robot to collapse into an uneven stance.
- **Dance/motion demo:** Run at least one demo mode and verify there is no repeated joint binding at the extremes of motion.
- **Repeatability:** Run the same short sequence three times and confirm behavior is consistent after each stop/start.

Pass criteria (practical):
- The robot completes a short forward/back cycle without a leg locking up.
- Motion looks symmetrical enough that it does not drift dramatically on a flat surface.
- No wires snag, and no fastener loosens visibly during the demo.

## Voice interaction test plan (support varies)

Because “voice interaction support” can differ by version, validate it as a controlled sequence:
1. Put the robot in a stable stance or lifted position.
2. Enable the voice mode using the kit’s provided resources for your revision.
3. Test a small set of commands/actions supported by your version and record what the robot does each time.
4. If voice triggers movement, repeat the test with the robot on a clear surface and be ready to power off.

## Troubleshooting guide (symptom → what to verify)

- **Robot turns instead of walking straight:** Verify left/right leg assemblies are mirrored correctly and that cables are not restricting one side.
- **One leg jitters or stalls:** Verify connectors are fully seated and that the joint can move freely by hand when unpowered.
- **Robot “hops” or scrapes:** Verify feet contact points and confirm no linkage is installed at an incorrect angle.
- **Demo works once then degrades:** Re-check fasteners, then inspect for cable tension that increases near end-of-travel.

## Demo media placeholders (add real files when available)

- `media/assembly-overview.mp4` — Placeholder clip showing the completed body before first power-on.
- `media/first-power-on-stand.mp4` — Placeholder clip demonstrating lifted first power-on and initial leg motion checks.
- `media/forward-back-test.mp4` — Placeholder clip of a short forward/back cycle on a flat surface.
- `media/dance-demo.mp4` — Placeholder clip of one dance/motion demo mode.
- `media/voice-trigger-demo.mp4` — Placeholder clip showing voice interaction triggering a safe, small action.

## Related

- Tutorial hub: https://feigen8n.online/tutorials/
- Kit page: https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/
- Product page: https://feigen8n.online/product/diy-voice-quadruped-robot-kit/
- Planned tutorial slug: `voice-quadruped-robot-assembly-guide`
