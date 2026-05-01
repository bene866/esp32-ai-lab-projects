Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

## SEO snapshot (audit-based)
**Audited URLs (`200 OK`, `ok=true`):**
- Tutorials hub: `https://feigen8n.online/tutorials/`
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description count: `1`; Canonical count: `1`
  - Headings: H1 = `Tutorials`, H2 count = `0`
  - Images: `0`; Internal links: `21`
  - Schema JSON-LD present: `false`
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description count: `2`; Canonical count: `1`
  - Headings: H1 = `STM32 Self-Balancing Car Kit`, H2 count = `9`
  - Images: `8` (missing alt: `0`); Internal links: `21`
  - Schema JSON-LD present: `false`
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project` (same as kit page)
  - Meta description count: `2`; Canonical count: `1`
  - Headings: H1 = `STM32 Self-Balancing Car Kit`, H2 count = `9`
  - Images: `8` (missing alt: `0`); Internal links: `21`
  - Schema JSON-LD present: `false`

**Key issues to review**
- Kit + product pages share the same title and meta description text (audit indicates duplicated intent).
- `meta_description_count=2` on both kit and product pages suggests duplicated meta output.
- No JSON-LD schema detected on any audited page.

## Generated files (today)
- `audit-insights.md` — audit table + duplication highlights (title/meta + missing schema).
- `tutorial-draft.md` — draft checklist: STM32 self-balancing car setup + PID calibration bring-up steps (review-required; slug: `stm32-self-balancing-car-setup`).
- `product-seo-review.md` — draft recommendations (not applied); seed: `feac300aa1ae2cbbe90517966488864212c2d2a184c0d46363113384d92c6f55`.
- `internal-link-suggestions.md` — draft link plan from kit/product pages to `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/` (publish only when target exists).
- `github-readme-update-draft.md` — README draft intent for repo dir `stm32-self-balancing-car`.

## GitHub README intent (repo: `stm32-self-balancing-car`)
- Position the repo as a verify-on-your-build bring-up + tuning guide for a STM32 two-wheel balancing car using IMU attitude sensing and encoder feedback.
- Emphasize a safe sequence: confirm IMU orientation/angle stability, motor polarity, encoder direction, then tune PID incrementally; keep optional modules (app/ultrasonic) out of the critical path until balance is stable.

## Risks / blockers (review-required)
- Potential broken-link risk if kit/product pages link to the tutorial URL before the tutorial exists.
- SEO duplication risk from shared title and duplicated meta description output on kit/product pages.
- Structured-data gap: audit shows no JSON-LD schema on tutorials/kit/product pages.
- Technical accuracy risk: tutorial + README are checklists and must not imply verified hardware behavior without real build confirmation.

## Next automated action (draft-only, no publishing)
1. Prepare the WordPress tutorial draft at `/tutorials/stm32-self-balancing-car-setup/` using `tutorial-draft.md` (keep review_required).
2. After the tutorial URL exists, stage the two internal links described in `internal-link-suggestions.md` on the kit + product pages.
3. Stage SEO edits from `product-seo-review.md` to differentiate kit vs product page intent and resolve duplicated meta description output; optionally add JSON-LD where appropriate (audit currently shows none).
