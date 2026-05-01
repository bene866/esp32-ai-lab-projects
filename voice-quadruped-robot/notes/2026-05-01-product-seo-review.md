# Product SEO Review — Voice Quadruped Robot (DIY Voice-Controlled Quadruped Robot Kit) — 2026-05-01

## Current-page observations (audit-based)
- Kit page (`https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/`): `200 OK`, title = “DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo”, meta description count = `2`, canonical count = `1`, H1 = “DIY Voice-Controlled Quadruped Robot Kit”, H2 count = `10`, images = `9` with `0` missing `alt`, internal links = `21`, JSON-LD schema = `false`.
- Product page (`https://feigen8n.online/product/diy-voice-quadruped-robot-kit/`): `200 OK`, title matches the kit page, meta description count = `2`, canonical count = `1`, H1 matches, H2 count = `10`, images = `9` with `0` missing `alt`, internal links = `21`, JSON-LD schema = `false`.

## Title and meta recommendations
- Keep the current H1, but make the kit page title and product page title intentionally different to reduce duplicate SERP snippets.
- Fix meta description count from `2` to `1` per page, and ensure each page uses a unique description to avoid duplicate snippet selection.
- Example kit-page title: “DIY Voice-Controlled Quadruped Robot Kit — Assembly Demo”.
- Example product-page title: “Voice-Controlled Quadruped Robot Kit — Walking & Dance Modes”.
- Example kit-page meta (single tag): “Hands-on quadruped robot kit with servo-driven legs, walking actions, dance modes, and voice interaction support. Includes controller board, wires, and assembly resources.”
- Example product-page meta (single tag): “Build a four-legged walking robot and test forward/backward and dance modes. Beginner-friendly STEM demo kit with voice interaction support and included assembly resources.”

## H1/H2 guidance
- Keep one H1, and convert repeated “Watch the assembly and movement demo” H2 usage into a single “Assembly & Movement Demo” section to reduce heading redundancy.
- Add one H2 that targets the tutorial intent, such as “Assembly and Movement Test Guide”, and link to the future tutorial slug `voice-quadruped-robot-assembly-guide` once it exists.

## FAQ ideas (for on-page FAQ + support)
- What tools are needed for assembly, and what is a reasonable first build checklist.
- How to confirm each leg moves correctly before running any walking action.
- What to do if one leg direction looks reversed or a joint binds during motion.
- Which surfaces work best for a first walking test, and how to reduce slipping.
- What “voice interaction support” means for this kit and what the user should expect in a basic demo.

## Schema recommendations
- Add JSON-LD `Product` (name, images, offers price/availability, and brand/site name), and add `FAQPage` for the FAQ block.
- Add `VideoObject` for the assembly/movement demo section and `BreadcrumbList` for navigation clarity.

## Publishing risks
- Duplicate meta descriptions (`count = 2`) can cause inconsistent SERP snippets and should be corrected before publishing changes.
- The kit and product pages currently share the same title and similar copy, which increases duplication risk and reduces keyword coverage across both URLs.
- “Voice interaction support” is a claim that should stay specific and bounded in wording to avoid customer expectation gaps.
