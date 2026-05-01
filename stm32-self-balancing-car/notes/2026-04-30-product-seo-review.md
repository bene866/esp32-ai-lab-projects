# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30

## Scope
Target pages:
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
Supporting hub:
- Tutorials hub: `https://feigen8n.online/tutorials/`
Related tutorial (already linked from hub and product pages): `/tutorials/stm32-self-balancing-car-setup/`

Primary keywords to cover naturally:
- “STM32 self balancing car kit”
- “self balancing robot PID tuning”
- “IMU robot car setup”

## Current-page observations (audit-based)
- Both kit and product pages return `200 OK` with `ok=true`.
- Title (kit + product): “STM32 Self-Balancing Car Kit | PID Control Robotics Project”.
- Meta description count (kit + product): `1` (no duplication detected).
- Canonical count (kit + product): `1`.
- H1 (kit + product): “STM32 Self-Balancing Car Kit” (matches product name).
- H2 count (kit + product): `11`, including “Related setup guides” and “STM32 self-balancing car setup and PID calibration checklist”.
- Images (kit + product): `8` with `0` missing `alt` (good baseline accessibility).
- Internal links (kit + product): `22` with visible commerce CTAs (Add to Cart / Buy Now) and navigation links.
- Schema JSON-LD (kit + product): `true` (present, but still worth validating type coverage and field completeness).
- Tutorials hub returns `200 OK`, has `0` images, `0` H2s, `has_schema_json_ld=false`, and includes an internal link to “STM32 self-balancing car setup and PID calibration checklist”.

## Search intent alignment
The stated search intent is “STM32 self-balancing robot setup, IMU checks, motor direction, PID tuning checklist”. The current kit/product pages already position the kit around PID control, IMU sensing, and encoder motors, and they already surface a setup guide entry. The main intent gap is likely “checklist depth” on the commercial pages, because the excerpt reads more like an overview and disclaimer than a task-driven, scannable bring-up flow.

## Title + meta recommendations
Keep the branding but sharpen intent coverage and keyword match.

Suggested title directions (choose one and keep it consistent on kit + product pages):
1) “STM32 Self-Balancing Car Kit — IMU & PID Tuning Project”
2) “STM32 Self-Balancing Car Kit | IMU Setup + PID Tuning Checklist”
3) “STM32 Self-Balancing Car Kit | Two-Wheel PID Balance Robot”

Suggested meta description direction (one sentence, action + proof points, avoid claims you cannot verify):
- “Build a two-wheel STM32 self-balancing robot and follow a practical IMU check + motor direction + PID tuning checklist. Includes IMU sensing, encoder motors, and a linked setup guide.”

## H1/H2 guidance
- Keep the current H1 unchanged, because it is clean and matches the product name.
- Reorder or rewrite H2s so the “Related setup guides” block appears above or near the first product photo, then add one new H2 that previews the checklist value without duplicating the full tutorial.
- Add an H2 specifically targeting intent phrasing, such as “Setup & PID calibration (what you will validate)”, and use short bullets under it (IMU orientation check, motor direction check, encoder feedback sanity check, safe first power-on, PID tuning loop).

## Copy gaps to close (without inventing hardware specifics)
- Add a “What you will verify before tuning” section that is observable and revision-agnostic (orientation, wiring continuity, direction checks), because the excerpt currently emphasizes variability and disclaimers but does not surface enough actionable checkpoints.
- Add “Who this kit is for” phrasing that matches “setup and PID calibration checklist” intent (learners who want a bring-up flow, not only a product spec list).
- Add a short “Troubleshooting entry points” block that routes to the tutorial for the full checklist, and keeps the product page scannable.

## Internal-link placements (specific and reviewable)
- On kit page and product page, keep the existing link to `/tutorials/stm32-self-balancing-car-setup/`, but adjust the surrounding sentence to include an intent phrase like “IMU checks, motor direction, and PID tuning checklist”.
- On the tutorial page (when editing that content), add two reciprocal links near the top and near the end:
  - Link back to the kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/` with an anchor like “STM32 self-balancing car kit”.
  - Link back to the product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/` with an anchor like “order the STM32 self-balancing car kit”.
- On the tutorials hub, the STM32 tutorial link already exists. Add one short contextual sentence under that card or list item (if the hub supports excerpts) that includes “PID tuning” and “IMU setup” phrasing.

## Official outbound reference opportunities
Add 1–2 outbound links where they help the reader complete setup tasks, not as generic footer links:
- “STM32Cube documentation” (`https://www.st.com/en/development-tools/stm32cubeide.html`) as a resource for IDE/project bring-up context.
- “ST motor control resources” (`https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html`) as background reading for motor control concepts that relate to tuning and stability work.

## Schema recommendations (validate and extend)
Because JSON-LD is present on kit/product pages, validate that it covers:
- `Product` with `name`, `image`, and an `offers` block that matches the visible pricing and “In stock” messaging from the excerpt.
- `BreadcrumbList` so the kit/product pages produce clean breadcrumb rich results.
- `Article` schema on the tutorial page (not the product page) to support “checklist” queries and improve eligibility for informational snippets.
If JSON-LD currently exists only as Product, add BreadcrumbList, and ensure only one primary Product entity is declared to avoid ambiguity.

## FAQ ideas (for intent capture and snippet eligibility)
Add 4–6 FAQs on the kit/product page that are phrased as setup questions, not specs you cannot guarantee:
- “What should I verify before attempting PID tuning?”
- “How do I confirm the IMU orientation is correct?”
- “What is the safe first power-on sequence for a balancing robot?”
- “How do I check motor direction before balancing?”
- “What is the simplest PID tuning order for a first stable stand?”

## Conversion risks to address
- The excerpt correctly warns that revisions vary, but if the page feels too disclaimer-heavy early on, it may reduce buyer confidence. Balance the disclaimer with a short, concrete “You will be able to validate these steps on your own hardware” checklist preview.
- Ensure the “setup guide” link is visible before the first purchase CTA for readers arriving from “PID tuning checklist” searches, because their first action is often to evaluate documentation quality.

## Prioritized fixes (highest impact first)
1) Update title/meta to include “IMU setup” and “PID tuning checklist” language while staying truthful and consistent across kit + product pages.
2) Add a scannable “Setup & PID calibration (what you will validate)” H2 section on kit + product pages with 5–7 revision-agnostic bullets.
3) Strengthen internal linking: product/kit ↔ tutorial cross-links with intent-matching anchors, and add a short descriptive line on the tutorials hub if supported.
4) Validate and, if needed, expand schema to include `BreadcrumbList` on kit/product pages and `Article` on the tutorial page.
5) Add setup-focused FAQs on the kit/product pages to capture “how to” queries without promising specific components or performance.
