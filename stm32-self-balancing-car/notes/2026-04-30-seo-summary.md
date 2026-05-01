Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

Uniqueness seed: `702b44edb2766457766ca4e37645d9699f48abfc3e8cfcaef34daa0b881b6cf6`

## SEO snapshot (audit-based)
- URLs audited (`200 OK`):  
  - `https://feigen8n.online/tutorials/`  
  - `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`  
  - `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Titles:  
  - Tutorials hub: `Tutorials – ESP32 AI Lab`  
  - Kit + Product: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
- Meta descriptions:  
  - Tutorials hub: present (`meta_description_count=1`)  
  - Kit + Product: duplicated (`meta_description_count=2`) with the same description text
- Canonical tags: present on all audited pages (`canonical_count=1`)
- Schema: JSON-LD not detected on all audited pages (`has_schema_json_ld=false`)
- Headings:  
  - Tutorials hub: `h1=["Tutorials"]`, `h2_count=0`  
  - Kit + Product: `h1=["STM32 Self-Balancing Car Kit"]`, `h2_count=9` (Order / Included / Features / Gallery / Shipping…)
- Images (kit/product pages): `image_count=8`, `missing_alt_count=0`  
  Tutorials hub: `image_count=0`

## Generated files (today’s run)
- `audit-insights.md` — audit findings summary for the three URLs
- `tutorial-draft.md` — draft tutorial: setup + PID calibration checklist (review-required)
- `product-seo-review.md` — SEO recommendations (not applied)
- `internal-link-suggestions.md` — planned links to `/tutorials/stm32-self-balancing-car-setup/` (not applied)
- `github-readme-update-draft.md` — README draft emphasizing checklist-style setup and tuning workflow

## GitHub README intent (draft)
- Positions the repo as documentation-first: setup notes + PID calibration checklist for a two-wheel STM32 balancing robot.
- Explicitly marks validation as not verified in this repo run (no bench-test claims) and lists items to confirm before publishing (assembly photos, wiring notes, build steps, tuning logs, demo media).

## Risks / constraints to review
- Duplicate meta description on both kit and product pages (`meta_description_count=2`) can dilute snippets and complicate SEO QA.
- No JSON-LD schema detected on audited pages (site-wide for this crawl scope), which limits rich result eligibility signals.
- The tutorial draft is intentionally non-assumptive (no fixed IMU/pin map/known-good gains); it needs completion and human verification before it can be linked from commerce pages.

## Next automated action (proposed)
- Complete `tutorial-draft.md` into a full checklist (mechanical preflight → first power-on → IMU/encoder sanity checks → PID tuning loop → optional app/ultrasonic sections), then create the WordPress draft at slug `stm32-self-balancing-car-setup` and apply the two internal links recommended in `internal-link-suggestions.md`, followed by a re-audit to confirm meta/schema/linking changes.
