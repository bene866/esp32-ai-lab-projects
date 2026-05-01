Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit  

# Daily SEO Summary — 2026-04-30

## SEO snapshot (audit-based)
- URLs checked (`200 OK`, `ok=true`):
  - `https://feigen8n.online/tutorials/`
  - `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Titles:
  - Tutorials hub: `Tutorials – ESP32 AI Lab`
  - Kit + Product: `STM32 Self-Balancing Car Kit | PID Control Robotics Project` (same on both pages)
- Meta / canonicals:
  - Kit: `meta_description_count=2`, `canonical_count=1`
  - Product: `meta_description_count=2`, `canonical_count=1`
  - Tutorials hub: `meta_description_count=1`, `canonical_count=1`
- Structured data:
  - All checked pages: `has_schema_json_ld=false`
- Headings / content structure:
  - Tutorials hub: `h1=["Tutorials"]`, `h2_count=0`
  - Kit + Product: `h1=["STM32 Self-Balancing Car Kit"]`, `h2_count=9` (sections include “What You Can Explore”, “What’s Included”, “Key Features”, “Notes / Disclaimer”, “Shipping & Quote”)
- Images / accessibility:
  - Tutorials hub: `image_count=0`
  - Kit + Product: `image_count=8`, `missing_alt_count=0`
- Internal links:
  - Tutorials hub: `internal_link_count=21`
  - Kit + Product: `internal_link_count=21`

## Generated files (today)
- `audit-insights.md` — crawl status + duplicated meta + missing JSON-LD callouts (scope: Tutorials hub + Kit + Product)
- `tutorial-draft.md` — WordPress draft checklist for setup + PID calibration (slug: `stm32-self-balancing-car-setup`, date: `2026-04-30`, review-required)
- `product-seo-review.md` — audit-grounded recommendations (Uniqueness seed: `3ea75862e301ff8f17e2ff046799322b24764393ccc4f248615753749725c0c3`)
- `internal-link-suggestions.md` — suggested routing between Kit/Product pages and the new tutorial slug
- `github-readme-update-draft.md` — README draft framing the repo as a verify-on-your-build setup + tuning checklist (no performance claims)

## GitHub README intent (repo: `stm32-self-balancing-car`)
- Position the project as a practical bring-up + calibration checklist for an STM32 two-wheel balancing kit using IMU sensing and encoder feedback, with optional ultrasonic/app-control notes.
- Keep language explicitly “draft / checklist / verify on your own build” to avoid implying measured results.

## Risks & constraints to keep visible
- **Duplicated meta descriptions** on both Kit and Product pages (`meta_description_count=2`) can dilute snippet control.
- **No JSON-LD** detected across the audited pages (`has_schema_json_ld=false`), limiting rich-result eligibility.
- **Hardware variability** (board/programming interface, sensor orientation, wiring polarity) means the tutorial must stay checklist-first and verification-driven.
- **Content safety**: avoid “balances out of the box” claims; keep “Notes / Disclaimer” cautious and prominent.

## Next automated action (proposed)
- After the `/tutorials/stm32-self-balancing-car-setup/` draft exists on-site, add the two suggested internal links from Kit + Product pages to that slug (anchors already drafted), then re-audit for meta-description duplication and schema JSON-LD presence before any publish step.
