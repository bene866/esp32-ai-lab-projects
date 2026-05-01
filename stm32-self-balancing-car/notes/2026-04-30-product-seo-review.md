# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30

Status: draft recommendations (not applied)  
Uniqueness seed: `702b44edb2766457766ca4e37645d9699f48abfc3e8cfcaef34daa0b881b6cf6`  
Focus: **STM32 self-balancing car setup and PID calibration checklist** (planned tutorial slug: `stm32-self-balancing-car-setup`)

## Pages reviewed (from provided audit)
- Tutorials hub: `https://feigen8n.online/tutorials/`
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Current-page observations (audit-based)

### Crawl / indexability basics
- All audited URLs: `200 OK` and `ok=true`.
- Canonical tags: present (`canonical_count = 1`) on all three audited pages.
- JSON-LD schema: not found (`has_schema_json_ld = false`) on all three audited pages.

### Titles & meta descriptions
- Tutorials hub title: `Tutorials – ESP32 AI Lab`
- Kit + Product page title (same on both): `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
- Kit + Product meta description text (same on both): “Explore a DIY STM32 self-balancing car kit with PID control, IMU attitude sensing, encoder motor feedback, app control, and hands-on robotics learning features.”
- **Meta description tag count**
  - Tutorials hub: `meta_description_count = 1`
  - Kit page: `meta_description_count = 2` (risk)
  - Product page: `meta_description_count = 2` (risk)

### Headings
- Kit + Product page H1: `STM32 Self-Balancing Car Kit`
- Kit + Product page H2 structure: `h2_count = 9`
  - Sample H2s: `Order This Kit`, `What You Can Explore`, `What’s Included`, `Key Features`, `Product Photo`, `Gallery`, `Notes / Disclaimer`, `Shipping & Quote`, `Need a different version?`
- Tutorials hub: `h1 = Tutorials`, `h2_count = 0`

### Images & accessibility
- Kit + Product: `image_count = 8`, `missing_alt_count = 0` (good)
- Tutorials hub: `image_count = 0`

### Internal links (pattern notes)
- Kit + Product: `internal_link_count = 21`, including repeated CTAs (`Add to Cart`, `Buy Now`) and global nav links (Home/Kits/Projects/About/Inquiry/Tutorials/Cart).
- Tutorials hub: `internal_link_count = 21` and lists multiple tutorial links.

## Title recommendations (kit + product pages)
Keep the current positioning (STM32 + self-balancing + PID), but consider tightening intent and adding one concrete hardware cue (IMU / encoder) to improve relevance for robotics learners.

Options (choose one per page; ideally make kit vs product slightly different):
1. `STM32 Self-Balancing Car Kit | PID + IMU + Encoder Feedback`
2. `STM32 Self-Balancing Robot Car Kit | PID Control Learning Project`
3. `STM32 Self-Balancing Car Kit | IMU Attitude + Encoder Motors + PID`

Notes:
- Avoid making both pages identical if both are indexable; slight differentiation helps reduce keyword cannibalization.

## Meta description recommendations (and the “count=2” fix)
### Priority fix
- Reduce to **exactly one** meta description tag on each of:
  - `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

### Fresh description drafts (pick one per page; don’t use the same copy twice)
**Kit page suggestion**
- “Build a two-wheel STM32 self-balancing robot and learn PID control with IMU attitude sensing, encoder motor feedback, app control, and an ultrasonic module for basic avoidance.”

**Product page suggestion**
- “A hands-on STM32 self-balancing car kit for robotics learning: PID tuning practice, IMU-based attitude sensing, encoder motors, ultrasonic obstacle features, plus source code and materials.”

## H1 / H2 guidance (focus: setup + PID calibration intent)
### H1
- Keep a single H1: `STM32 Self-Balancing Car Kit` (already correct).

### H2 improvements (add one “practical setup” section without turning the product page into a full tutorial)
Current H2s are mostly ecommerce navigation (order/included/features/gallery/shipping). To support the query “setup and PID calibration checklist”, add **one** high-signal section and link out to the full tutorial.

Recommended new H2 candidates (choose 1–2):
- `Setup Checklist (Before First Power-On)`
- `PID Calibration Checklist (Quick Start)`
- `Troubleshooting: Won’t Balance / Oscillation / Drift`

Within that section, keep content short and checklist-style, then add a prominent internal link to the planned tutorial path:
- `/tutorials/stm32-self-balancing-car-setup/` (once it exists)

## FAQ ideas (ready-to-write, audit-consistent)
If you add an FAQ block, keep answers factual and aligned with the current page claims (PID, IMU, encoder feedback, app control, ultrasonic module, source code/materials, intermediate level, shipping varies).

Suggested FAQ questions:
1. “How does the STM32 self-balancing car keep its balance?”
2. “What’s the role of the IMU attitude sensing module in this kit?”
3. “Why are encoder motors used for feedback?”
4. “Does the kit support app control out of the box?”
5. “What can I do with the ultrasonic module (avoidance / following)?”
6. “Is source code included with the kit?”
7. “What skill level is this kit designed for?”

## Schema recommendations (JSON-LD)
Schema is currently missing on all audited pages. Add JSON-LD to improve eligibility for rich results and to clarify page intent.

Recommended schema types:
- `Product` on kit + product pages (name, description, images, brand/site name, and **offers that match the live on-page price/availability**).
- `FAQPage` only if an on-page FAQ section is published.
- `BreadcrumbList` to reinforce site structure (Home → Kits → STM32 Self-Balancing Car Kit, etc.).
- Optional (site-wide): `WebSite` (and search action if relevant to your theme setup).

## Internal linking recommendations (minimal, ecommerce-friendly)
- From kit + product pages: add one contextual link near the “What You Can Explore” or “Notes / Disclaimer” area pointing to `/tutorials/stm32-self-balancing-car-setup/` with an anchor like:
  - “STM32 self-balancing car setup & PID calibration checklist”
- From the new tutorial (once drafted): link back to the kit page (`/kits/stm32-self-balancing-car-kit/`) and product page (`/product/stm32-self-balancing-car-kit/`) with clear “Buy / parts list / what’s included” anchors.

## Publishing risks to flag before pushing changes
- **Duplicate meta description tags** (`meta_description_count = 2`) on both kit and product pages can cause inconsistent snippets and is a straightforward technical SEO fix.
- **Near-duplicate content risk**: kit and product pages share the same title and meta description (and appear structurally similar). If both are indexable, they may compete for the same queries; differentiate intent or ensure the canonical strategy is deliberate.
- **No JSON-LD**: missing structured data reduces the chance of enhanced SERP features (Product/FAQ rich results).
- **CTA repetition** (multiple `Add to Cart` / `Buy Now` links): not inherently bad, but keep an eye on UX clutter and ensure the primary informational path (setup/PID) is easy to find without scrolling past repeated purchase blocks.

## Recommended change set (fastest wins first)
1. Fix meta description duplication (ensure exactly one per page).
2. Add JSON-LD `Product` schema (and `BreadcrumbList`).
3. Add a short “Setup/PID checklist” H2 section + link to the planned tutorial.
4. Publish an FAQ block + `FAQPage` schema (only if FAQ is live).
5. Differentiate kit vs product title/meta to reduce overlap.
