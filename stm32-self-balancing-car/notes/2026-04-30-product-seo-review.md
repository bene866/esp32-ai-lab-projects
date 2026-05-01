# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30
Status: draft recommendations (not applied)  
Uniqueness seed: `feac300aa1ae2cbbe90517966488864212c2d2a184c0d46363113384d92c6f55`

## Current-page observations (audit-based)
- `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`: `200 OK`, title = “STM32 Self-Balancing Car Kit | PID Control Robotics Project”, meta description count = `2`, canonical count = `1`, JSON-LD schema = `false`.
- `https://feigen8n.online/product/stm32-self-balancing-car-kit/`: `200 OK`, same title as kit page, meta description count = `2`, canonical count = `1`, JSON-LD schema = `false`.
- H1 is present on both kit/product pages: “STM32 Self-Balancing Car Kit”.
- H2 count on both kit/product pages is `9` (includes “Order This Kit”, “What You Can Explore”, “What’s Included”, “Key Features”, “Notes / Disclaimer”, “Shipping & Quote”).
- Images: `8` with `0` missing alt on both kit/product pages.
- Tutorials hub `https://feigen8n.online/tutorials/`: `200 OK`, H1 = “Tutorials”, H2 count = `0`, images = `0`, JSON-LD schema = `false`.

## Title + meta recommendations
- Keep separate intent between the kit page and product page to reduce duplication, because both currently share the same title and description theme.
- Suggested title pattern (choose one per page):
  - Kit page: “STM32 Self-Balancing Car Kit — Setup + PID Tuning Starter Kit”
  - Product page: “STM32 Self-Balancing Car Kit — PID, IMU, Encoders, App Control”
- Reduce meta descriptions to exactly one per page and make them distinct; mention only audited features (PID, IMU attitude sensing, encoder feedback, app control, ultrasonic module, learning materials).

## H1/H2 guidance
- Keep a single H1 (“STM32 Self-Balancing Car Kit”) and add 2–3 new H2 sections aligned to the focus topic:
  - “Setup Checklist (First Power-On)”
  - “IMU Orientation + Calibration Notes”
  - “PID Calibration Checklist (Stability → Response → Drift)”
- Add one internal link block: “Build guide: `/tutorials/stm32-self-balancing-car-setup/`” (only after the tutorial exists as a draft).

## FAQ ideas (safe, audit-aligned)
- “What should I verify before the first power-on?”
- “How do I approach PID tuning for a two-wheel balancing robot?”
- “What are common IMU mounting or orientation mistakes to check?”
- “How do encoders help stability and speed control?”
- “What does the ultrasonic module enable in this kit?”
- “What is included in the kit, and what is not included?”

## Schema recommendations
- Add JSON-LD on kit/product pages (currently absent): `Product` (price, sale price, availability), plus optional `FAQPage` if FAQ is added, and `BreadcrumbList` if breadcrumbs exist on the site.

## Publishing risks
- Duplicate meta description tags (`count = 2`) can cause inconsistent snippets.
- Near-duplicate title/positioning between kit vs product pages can dilute relevance and split ranking signals.
- Adding a tutorial link before the tutorial is published can create broken internal links.
