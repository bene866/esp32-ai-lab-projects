---
status: draft
date: 2026-04-30
project_key: stm32-self-balancing-car-kit
project_name: "STM32 Self-Balancing Car Kit"
review_required: true
not_applied: true
uniqueness_seed: "828dbc3eaa93cc7201a28154edc7e4ba3a64c4c0674825c8fd8ad4d23b3311db"
---

# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30

## Scope (audit-based)
Reviewed URLs from the provided crawl:

- Tutorials hub: `https://feigen8n.online/tutorials/` (200 OK)
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/` (200 OK)
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/` (200 OK)

Focus topic for the next tutorial: **STM32 self-balancing car setup and PID calibration checklist** (planned slug: `stm32-self-balancing-car-setup`).

---

## Audit snapshot (current state)

### Tutorials hub — `https://feigen8n.online/tutorials/`
- Title: `Tutorials – ESP32 AI Lab`
- Meta description: present (`count=1`)
- Canonical: present (`count=1`)
- Headings: H1 = `Tutorials`; H2 count = `0`
- Images: `0` (alts missing: `0`)
- Internal links: `21`
- Schema JSON-LD: **not detected**

### Kit page — `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
- Meta description: **duplicate present** (`count=2`)
- Canonical: present (`count=1`)
- Headings: H1 = `STM32 Self-Balancing Car Kit`; H2 count = `9`
  - H2 samples: `Order This Kit`, `What You Can Explore`, `What’s Included`, `Key Features`, `Product Photo`, `Gallery`, `Notes / Disclaimer`, `Shipping & Quote`, `Need a different version?`
- Images: `8` (alts missing: `0`)
- Internal links: `21` (includes add-to-cart / buy-now links)
- Schema JSON-LD: **not detected**
- On-page excerpt includes: launch price section (regular vs current), “In stock”, and a feature/contents list (IMU, encoders, ultrasonic, app control, source code/materials).

### Product page — `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
- Meta description: **duplicate present** (`count=2`)
- Canonical: present (`count=1`)
- Headings and sections: match the kit page snapshot (H1 same; H2 count `9`)
- Images: `8` (alts missing: `0`)
- Internal links: `21`
- Schema JSON-LD: **not detected**

---

## Key observations (what to keep / what to fix)
1) **Meta description duplication** is the clearest technical SEO issue on both the kit and product URLs (`meta_description_count=2`).  
2) **Kit and product pages appear highly similar** (same title, same meta description text, same H1, same H2 set, similar excerpt). Even with a canonical present, this can blur ranking signals unless each page has a distinct purpose and copy.  
3) **Headings are already structured** on the kit/product pages (H2 sections cover ordering, features, gallery, disclaimers, shipping). That’s a solid baseline to extend with setup/tuning intent.  
4) **No JSON-LD schema detected** across all audited pages. This is an opportunity for richer SERP understanding (Product/FAQ/Breadcrumbs).

---

## Title & meta recommendations (actionable edits)

### Keep the current title concept, but tighten “setup intent” targeting
Current title (both kit + product): `STM32 Self-Balancing Car Kit | PID Control Robotics Project`

Recommended variants (pick one per page; do not use the same title on both):
- **Kit page title option:** `STM32 Self-Balancing Car Kit | IMU + Encoder PID Balancing Robot`
- **Product page title option:** `STM32 Self-Balancing Car Kit | PID Control Robotics Project (In Stock)`

Rationale (audit-based): the pages already emphasize **PID**, **IMU attitude sensing**, and **encoder feedback** in their excerpt; differentiating titles helps reduce page-to-page duplication while staying aligned with the existing content.

### Fix meta description count (must be exactly 1)
Current: meta descriptions duplicated (`count=2`) on kit + product pages.

Recommended meta description drafts (choose one per page; keep them different):
- **Kit page meta (feature-forward):**  
  “Build a two-wheel STM32 self-balancing robot and explore PID control with IMU attitude sensing, encoder motor feedback, app control, and an ultrasonic module. Includes chassis, wiring, and learning materials.”
- **Product page meta (purchase-forward):**  
  “STM32 Self-Balancing Car Kit for hands-on PID robotics learning: IMU attitude sensing, encoder motors, app control support, ultrasonic function, and included materials. See pricing, shipping quote, and what’s included.”

---

## H1 / H2 guidance (on-page structure)

### H1
- Keep H1 as-is: `STM32 Self-Balancing Car Kit` (already clear and consistent).

### Add 1–2 new H2 sections to capture “setup + PID calibration checklist” intent
The current H2 set is commerce- and overview-oriented. To support the planned tutorial topic and improve relevance, add:

- **New H2:** `Setup & PID Calibration Checklist`  
  - Bullet checklist placeholders (no claims): IMU orientation check, encoder direction sanity check, balance target angle note, PID tuning pass order, safety notes for first lift test.
- **New H2:** `Common Tuning Symptoms (Quick Diagnosis)`  
  - Examples phrased as “If you see X, try Y” (no hardware verification claims).

Placement suggestion: between `Key Features` and `Notes / Disclaimer` so it’s visible before shipping/legal sections.

---

## FAQ ideas (FAQPage-ready, draft questions only)
Use questions that match what the page already mentions (PID, IMU, encoders, app control, ultrasonic, included materials):

1) What should I check before the first power-on of the balancing car?  
2) How do I confirm the IMU module orientation is correct for balancing?  
3) What’s the simplest way to verify encoder direction and motor direction match?  
4) In what order should I tune PID for a two-wheel self-balancing robot?  
5) What does “app control support” mean on this kit page?  
6) How is the ultrasonic module used (avoidance / following) and when should I enable it?  
7) What’s included in the box (and what’s not)?  
8) Where do I request a shipping quote or a different version?

---

## Schema recommendations (JSON-LD to add)
Audit shows `has_schema_json_ld: false` on all reviewed URLs.

Suggested schema types:
- **Product** (on kit + product pages): include name, page URL, and a concise description aligned with the excerpt (PID, IMU, encoders, ultrasonic, learning materials).  
- **FAQPage** (on whichever page gets the FAQ section).  
- **BreadcrumbList** (sitewide pattern, if available) for clearer hierarchy between Tutorials / Kits / Products.  
- **WebSite / Organization** (sitewide, if not already present elsewhere) to standardize brand signals.

---

## Internal linking (small changes with clear intent)
- Add a single “build guide” style link from the kit/product pages to the future tutorial URL once it exists:  
  - Target: `/tutorials/stm32-self-balancing-car-setup/`  
  - Suggested anchor: `STM32 self-balancing car setup and PID calibration checklist`
- On `https://feigen8n.online/tutorials/`, add an entry pointing to the new tutorial once published (the hub already has 21 internal links and lists other guides, but has no H2 sections; a small “Robotics / Control” grouping could justify new subheadings later).

---

## Publishing risks & review checklist (before applying)
- **Duplicate meta descriptions (count=2)**: fix first; it’s a concrete, audit-confirmed issue.  
- **High similarity between kit and product pages**: avoid using identical titles/meta on both; consider giving each page a distinct role (overview vs purchase vs setup help).  
- **Don’t over-promise**: the excerpt mentions “source code and learning materials” and “app control support”; ensure any added copy stays factual and doesn’t imply verified performance or testing.  
- **Schema accuracy**: only encode claims that are already present on-page (PID, IMU, encoders, ultrasonic, included materials, price language if shown).  
- **Tutorial dependency**: don’t add internal links to `/tutorials/stm32-self-balancing-car-setup/` until the tutorial draft exists, to avoid dead links.
