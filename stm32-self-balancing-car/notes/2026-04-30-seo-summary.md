Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

## SEO snapshot (audit-based)
- Crawled `200 OK` (`ok=true`):
  - `https://feigen8n.online/tutorials/`
  - `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Indexability signals in audit:
  - All three pages show `canonical_count: 1`.
- Tutorials hub (`/tutorials/`):
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description count: `1` (audit excerpt appears truncated/long; full text not verified here)
  - Structure: `h1=["Tutorials"]`, `h2_count=0`, `image_count=0`, `has_schema_json_ld=false`
  - Internal links: `23`, including a link to `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/` with anchor “STM32 self-balancing car setup and PID calibration checklist”.
- Kit + Product pages (both audited):
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description count: `1`, canonical count: `1`
  - Structure: `h2_count=11`, `image_count=8`, `missing_alt_count=0`, `has_schema_json_ld=true`
  - Note: kit and product pages share the same title + meta description in the audit (duplication risk across URLs).

## Generated files (today)
- `audit-insights.md` — audit recap for the 3 URLs and what can/can’t be concluded from the provided crawl fields.
- `tutorial-draft.md` — checklist-style bring-up flow for IMU sanity, motor direction, encoder checks, and safe PID tuning (revision-agnostic language).
- `product-seo-review.md` — audit-based on-page review of kit/product pages plus discovery notes for the Tutorials hub.
- `internal-link-suggestions.md` — internal + external link plan centered on routing buyers/readers between kit/product pages and the tutorial.
- `github-readme-update-draft.md` — README draft positioning the repo as a pass/fail bring-up + tuning checklist (not a universal firmware promise).

## GitHub README intent (repo: `stm32-self-balancing-car`)
- Provide a repeatable validation sequence (sensing → actuation → closed-loop) aimed at isolating common balance failures (axis/sign, direction, encoder noise, power integrity, unstable gains) without assuming a specific kit revision.

## Risks / watchouts
- Hardware and wiring revisions vary by seller/revision; copy must stay “verify on your own hardware” and avoid guaranteed tuning outcomes.
- Duplicate title/meta between kit and product URLs may dilute SERP differentiation for similar queries.
- Tutorials hub has no H2s/images/schema in the audit; it may provide limited topical context beyond link anchors.

## Next automated action
- Prepare a WordPress draft for `slug: stm32-self-balancing-car-setup` using `tutorial-draft.md`, then stage a repo README update PR using `github-readme-update-draft.md` (no publishing/merging in this step).
