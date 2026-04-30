# Product SEO Review – STM32 Self-Balancing Car Kit – 2026-04-30  
Status: draft recommendations (not applied)  
Focus: **STM32 self-balancing car setup and PID calibration checklist** (planned tutorial slug: `stm32-self-balancing-car-setup`)

## Pages reviewed (from provided audit)
- Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/ (200)
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/ (200)
- Tutorials index (related hub): https://feigen8n.online/tutorials/ (200)

---

## Current-page observations (audit-based)

### 1) Kit page (`/kits/stm32-self-balancing-car-kit/`)
- Title: **“STM32 Self-Balancing Car Kit | PID Control Robotics Project”**
- Meta description: **count = 2** (duplicate meta description tags present)
- Canonical: **count = 1**
- H1: **“STM32 Self-Balancing Car Kit”**
- H2: **count = 9** (includes “Order This Kit”, “What You Can Explore”, “What’s Included”, “Key Features”, “Notes / Disclaimer”, “Shipping & Quote”, etc.)
- Images: **8**, missing alt: **0**
- Internal links: **21** (includes repeated “Add to Cart” / “Buy Now” anchors)
- Structured data: **no JSON-LD detected**
- On-page copy mentions: PID control, IMU attitude sensing, encoder motor feedback, app control support, ultrasonic function, source code/learning materials; shows launch pricing ($99 current, $129 regular) and “In stock”.

### 2) Product page (`/product/stm32-self-balancing-car-kit/`)
- Title: **same as kit page**
- Meta description: **count = 2** (same issue)
- Canonical: **count = 1**
- H1 / H2 structure: **matches kit page** (H2 count = 9)
- Images: **8**, missing alt: **0**
- Internal links: **21**
- Structured data: **no JSON-LD detected**
- Excerpt content appears effectively duplicated vs kit page (same positioning, features, pricing callouts).

### 3) Tutorials index (`/tutorials/`)
- Title: **“Tutorials – ESP32 AI Lab”**
- Meta description: **count = 1**
- Canonical: **count = 1**
- H1: **“Tutorials”**, H2: **0**
- Images: **0**
- Structured data: **no JSON-LD detected**
- Internal links: **21** (lists multiple tutorial entries)

---

## Priority fixes (highest SEO impact)

1) **Fix duplicate meta description tags (both kit + product pages)**
- Current state: `meta_description_count = 2` on both URLs.
- Recommendation: ensure **exactly one** meta description tag per page; keep it unique per URL (avoid the kit and product pages sharing the same description).

2) **Differentiate kit vs product page intent (reduce near-duplicate signals)**
- Current state: same title + same meta description text + highly similar sections on both URLs.
- Recommendation:
  - Give each URL a **distinct title + meta description** aligned to intent:
    - **Kit page**: learning/overview (features, what’s included, who it’s for).
    - **Product page**: purchase intent (what’s in the box, compatibility expectations, shipping/quote, support boundaries).
  - If the site platform supports it, keep one as the primary “canonical” content source and make the other meaningfully different (or consolidated), while preserving the single canonical tag count per page.

3) **Add JSON-LD (Product + FAQ)**
- Current state: `has_schema_json_ld = false` across all audited pages.
- Recommendation: add JSON-LD on kit/product pages to improve eligibility for rich results and clarify page type.

---

## Title + meta description recommendations

### Kit page (`/kits/stm32-self-balancing-car-kit/`)
**Proposed title options (pick one):**
- Option A: `STM32 Self-Balancing Car Kit – IMU + Encoder PID Robotics Learning`
- Option B: `STM32 Self-Balancing Robot Car Kit – PID Control, IMU Sensing, Encoders`

**Proposed meta description (single tag, ~1–2 sentences):**
- `Build a two-wheel STM32 self-balancing robot and learn PID tuning with IMU attitude sensing and encoder motor feedback. Includes kit parts, learning materials, and optional ultrasonic/app control features.`

### Product page (`/product/stm32-self-balancing-car-kit/`)
**Proposed title options (pick one):**
- Option A: `Buy STM32 Self-Balancing Car Kit – PID Robot Kit (In Stock)`
- Option B: `STM32 Self-Balancing Car Kit for PID Practice – Kit Contents + Shipping`

**Proposed meta description (single tag, purchase-focused):**
- `DIY STM32 self-balancing car kit with IMU sensing and encoder feedback for PID control practice. Review what’s included, pricing, and shipping/quote notes before ordering.`

---

## H1 / H2 guidance (structure + keyword coverage)

### Keep
- H1 is already clear and consistent: **“STM32 Self-Balancing Car Kit”**.

### Improve H2 usefulness for search + scanning
Current H2 set is e-commerce oriented. To support the planned tutorial topic (setup + PID calibration checklist), add one or two sections that bridge product intent to build intent without claiming lab-verified performance.

**Suggested H2 additions (kit page preferred):**
- `Setup Checklist (Before First Power-On)`
- `PID Calibration Checklist (First Stable Balance)`
- `Common Tuning Symptoms (Quick Diagnosis)`

**Suggested H2 adjustments (optional wording refresh):**
- “What You Can Explore” → consider `What You’ll Learn (PID + IMU + Encoders)`
- “Notes / Disclaimer” → consider `Safety & Tuning Notes` (keeps disclaimers but reads less generic)

---

## FAQ ideas (draft question list)
Use these as on-page FAQs (short, factual, and aligned to what’s already stated on the page):

1) What does a self-balancing robot use to stay upright (IMU + PID control)?
2) What feedback signals are used (IMU attitude + encoder motor feedback)?
3) What’s included in the kit (chassis, IMU module, encoder motors, ultrasonic module, battery holder/wiring, source code/learning materials)?
4) Is app control supported, and what can it do?
5) What does the ultrasonic module enable (obstacle avoidance/following functions)?
6) What are the first tuning steps if the robot oscillates or falls immediately?
7) What should I check before first power-on (wiring, polarity, mechanical alignment)?
8) Where should I start if I want a step-by-step setup + PID calibration checklist (link to the planned tutorial)?

---

## Schema (JSON-LD) recommendations
Add schema where it matches page intent and available data:

- **Product schema** (kit + product pages)
  - Include: name, description, images, offers (price), availability (“In stock” is shown in excerpt), and canonical URL.
- **FAQPage schema** (if FAQs are added)
  - Use a concise set of Q/A aligned to on-page content.
- **BreadcrumbList schema** (sitewide or on these pages)
  - Helps clarify hierarchy: Home → Kits/Product → STM32 Self-Balancing Car Kit.

---

## Internal linking recommendations (practical)
- From kit/product pages, add a contextual link near “Source code and learning materials” or “Notes”:
  - Link to planned tutorial: `/tutorials/stm32-self-balancing-car-setup/` (once published)
- From the tutorial (when drafted), link back to:
  - Kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
  - Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- From Tutorials hub (`/tutorials/`), add the new tutorial entry once available to strengthen discovery from an existing internal-link hub.

---

## Publishing risks / things to verify before applying changes
- **Duplicate meta descriptions (count = 2)**: resolve first; it’s a clear technical SEO issue.
- **Near-duplicate kit vs product pages**: identical titles/descriptions risk cannibalization; differentiate or consolidate intent.
- **No JSON-LD detected**: adding schema is safe, but verify it matches visible content (avoid adding claims not shown on-page).
- **CTA anchor repetition** (“Add to Cart” / “Buy Now” duplicates): not fatal, but consider reducing duplicate link blocks if the theme is outputting them twice (helps crawl efficiency and UX).
- **Tutorial promise risk**: if you reference the setup/PID checklist tutorial on product pages, ensure the draft exists (or mark it clearly as “coming soon”) to avoid broken links.
