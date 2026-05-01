# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30

## Current-page observations (from provided audit)
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/` → `200 OK`, meta description count = `2`, canonical count = `1`, JSON-LD schema = `false`.
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/` → `200 OK`, meta description count = `2`, canonical count = `1`, JSON-LD schema = `false`, title matches kit page.
- Both kit/product pages: H1 present (“STM32 Self-Balancing Car Kit”), H2 count = `9`, images = `8` with `0` missing alt.
- Tutorials hub: `https://feigen8n.online/tutorials/` → H2 count = `0`, images = `0`, JSON-LD schema = `false`.

## Title + meta recommendations (safe wording)
- Separate intent between kit vs product pages to reduce duplication.
- Ensure each page renders exactly one meta description tag.
- Meta description copy should avoid exact “box contents” claims unless the listing on that page explicitly guarantees them; use “features you can explore” framing instead.
  - Examples of safe topics (if the page copy supports them): PID tuning, IMU-based tilt sensing, encoder feedback, optional app/remote control (varies by listing).

## On-page structure recommendations
- Keep one H1, then add 2–3 H2 sections aligned to search intent:
  - “First Power-On Checklist”
  - “IMU Orientation and Sign Checks”
  - “PID Tuning Workflow (P → D → I)”
- Add one internal link block to the tutorial once published: `/tutorials/stm32-self-balancing-car-setup/` (do not link early if it would 404).

## FAQ ideas (avoid unverified kit contents)
- “What should I verify before first power-on?”
- “How do I check IMU orientation and sign?”
- “How do encoders help with stability and drift control?”
- “What should I do if the robot runs away immediately?”
- “Which parts vary by seller/listing, and how do I confirm mine?”

## Schema recommendations (audit gap)
- Add JSON-LD where missing: `Product` (use listing-backed fields only), plus optional `FAQPage` if FAQs are added, and `BreadcrumbList` if breadcrumbs exist.

## Publishing risks (audit-based)
- Duplicate meta descriptions can cause inconsistent snippets.
- Kit vs product page duplication can blur intent.
- Broken internal links if tutorial URLs are added before publish.
