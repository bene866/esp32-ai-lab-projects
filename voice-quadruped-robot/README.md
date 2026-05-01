# Voice Quadruped Robot (DIY Voice-Controlled Quadruped Robot Kit)

A hands-on quadruped robot build focused on **servo-driven leg motion**, **basic walking actions (forward/backward)**, **dance/motion demo modes**, and **voice interaction support**.

## Validation Status (as of 2026-05-01)

- This README is a **draft for human review**.
- Assembly, wiring, and movement steps below are **checklists** and **not a claim of completed hardware validation**.
- Replace placeholders (media, pin/wire labels, board details) only after verifying against your specific kit revision.

## What this project covers

- Mechanical assembly notes for a four-legged robot body
- Wiring + bring-up checklist for a servo-driven leg mechanism + controller board + connection wires
- Movement test guide (walk + demo modes) with a repeatable observation log
- A place to attach real photos/video used for support and documentation

## What’s included (kit-level reference)

- Quadruped robot body parts  
- Servo-driven leg mechanism  
- Controller board  
- Connection wires  
- Assembly and demo resources  

## Safety & handling

- Keep the robot **off the table edge**; first power-on should be on a stand so legs can move freely.
- Servos can draw high current; avoid repeatedly stalling joints at end stops.
- Power off before changing horns, repositioning linkages, or re-plugging servo leads.
- Route wires for strain relief so leg motion cannot pull connectors loose.

## Assembly checklist (mechanical)

1. **Inventory + identify parts**
   - Group body panels/frames, leg linkages, fasteners, servo horns, and wiring.
   - Separate each leg’s parts so you can build consistent left/right pairs.

2. **Dry-fit body structure**
   - Confirm mounting holes align before fully tightening.
   - Leave final tightening until all legs are attached and aligned.

3. **Leg build consistency**
   - Build one leg fully, then mirror the same sequence for the other three.
   - Visually confirm that front legs match each other, and rear legs match each other.

4. **Servo horn alignment (neutral-first workflow)**
   - Goal: assemble with joints near their **mid-range** so walking doesn’t immediately hit end stops.
   - If your controller provides a “center/neutral” function, use it before fixing horn positions.
   - If not, mark an approximate neutral orientation and keep adjustments small until you can command test movements.

5. **Final alignment**
   - Check that each leg has similar “rest” posture.
   - Confirm linkages don’t bind through the expected swing range.

## Wiring & power checklist

- **Label everything first**
  - Tag each servo lead with a leg ID (Front-Left / Front-Right / Rear-Left / Rear-Right) and joint ID (Hip/Knee/etc. as applicable).
- **Connector orientation**
  - Ensure consistent plug orientation across all servo channels; do not assume color order is universal.
- **Cable routing**
  - Route cables away from moving linkages; add slack loops for joints that rotate.
- **Power sanity**
  - Use the correct power input for the controller/servo system (exact voltage/current depends on your kit revision—document it once verified).
  - If using separate supplies for logic + servos, verify grounds are correctly referenced (only if your design requires it—confirm with your hardware docs).

## First power-on (bring-up sequence)

1. **No-load motion check**
   - Place the robot on a stand (legs not touching the ground).
   - Power on and watch for immediate jitter or aggressive movement.
2. **Single-joint test**
   - Trigger the smallest motion command available.
   - If a joint moves the wrong direction or hits a hard stop quickly: power off and correct horn/indexing or linkage orientation.
3. **Per-leg verification**
   - Confirm each leg responds and returns to a stable rest pose.
4. **Thermal/current warning signs**
   - Buzzing + heat + no motion typically indicates a stall or binding linkage—stop and re-check mechanics.

## Movement test guide (walk + demo modes)

Use this as a repeatable test log. The goal is to verify behavior without “tuning by vibes”.

### Test A — Basic forward/backward

- **Surface**: flat, with moderate grip
- **Start pose**: stable rest, legs symmetric
- **Run**: forward for 3–5 seconds, stop, then backward for 3–5 seconds
- **Log**
  - Drift direction (left/right)
  - Foot slip vs. lift consistency
  - Any leg that “lags” or over-steps
  - Any joint hitting an end stop

### Test B — Dance / motion demo modes

- Run the demo once, then again after a 1–2 minute rest.
- Log
  - Reproducibility (same motion each run?)
  - Peak wobble points
  - Any audible stall/buzz during repeated cycles

### Test C — Voice interaction support (functional check)

- Confirm that voice interaction can trigger a **known** action (e.g., start/stop, mode change).
- Log
  - Trigger reliability (missed/false triggers)
  - Latency from command → motion
  - Whether motion mode changes are safe (no sudden lurch)

## Troubleshooting quick map

- **Robot jitters at idle**: check mechanical binding, cable strain, or servo indexing; reduce load before re-testing.
- **One leg behaves differently**: swap that leg’s servo connection with a known-good channel (document the result) to isolate wiring vs. mechanical issues.
- **Frequent stalls at extremes**: re-center horn positions and reduce commanded range until alignment is corrected.
- **Unstable walking**: confirm all legs are mirrored correctly and that rest posture is symmetric before changing any control parameters.

## Demo media placeholders (add real assets later)

Add real media and update links once captured:

- `media/assembly-overview.jpg` — full kit layout + labeled parts
- `media/wiring-closeup.jpg` — controller board + servo connectors + labels
- `media/first-power-on.mp4` — on-stand bring-up (no-load)
- `media/walk-forward-backward.mp4` — basic walking test (flat surface)
- `media/dance-demo.mp4` — demo mode run
- `media/voice-trigger.mp4` — voice command triggers a specific action

## Reviewer checklist (fill in after verification)

- Controller board model / revision: `TBD`
- Power input requirements used in your build: `TBD`
- Servo count + joint naming used in this repo: `TBD`
- Any kit-specific assembly pitfalls (photo + note): `TBD`
- Confirmed list of motion modes available: `TBD`
- Voice interaction: supported commands and expected behavior: `TBD`

## Related

- Kit page: https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/
- Product page: https://feigen8n.online/product/diy-voice-quadruped-robot-kit/
- Tutorials hub: https://feigen8n.online/tutorials/
- Planned tutorial slug (draft target): https://feigen8n.online/tutorials/voice-quadruped-robot-assembly-guide/
