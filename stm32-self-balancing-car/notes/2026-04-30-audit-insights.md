# SEO Audit Report — STM32 Self-Balancing Car Kit (2026-04-30)

## Scope (provided crawl)
- `https://feigen8n.online/tutorials/`
- `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Crawl status
- All three URLs returned `200 OK` (`ok=true`).

## What this audit can (and can’t) confirm
- This report reflects crawl-extracted page structure signals (titles, counts, headings, links, basic flags).
- It does **not** prove specific kit contents, firmware availability, media, pricing, stock, or performance outcomes unless that exact text/evidence is provided in the audit context.

## Titles & meta descriptions
- Tutorials hub
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description: present (`count=1`)
- Kit page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present but duplicated (`count=2`)
- Product page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present but duplicated (`count=2`)
- Canonicals
  - All pages show exactly one canonical (`canonical_count=1`).

## Headings
- Tutorials hub: H1 `Tutorials`; no H2 headings (`h2_count=0`).
- Kit page: H1 `STM32 Self-Balancing Car Kit`; `h2_count=9` with sections including “What You Can Explore”, “What’s Included”, “Key Features”, and “Shipping & Quote”.
- Product page: same headline structure as kit page (`h2_count=9`).

## Images
- Tutorials hub: `image_count=0`.
- Kit page: `image_count=8`; `missing_alt_count=0`.
- Product page: `image_count=8`; `missing_alt_count=0`.

## Internal links
- Tutorials hub: `internal_link_count=21` (nav + multiple `/tutorials/.../` entries).
- Kit page: `internal_link_count=21` (commerce + nav).
- Product page: `internal_link_count=21` (commerce + nav).

## Structured data (schema)
- No JSON-LD detected on any audited page (`has_schema_json_ld=false`).

## Prioritized actions (next)
1. Fix duplicate meta descriptions on both STM32 pages (`meta_description_count=2`) by leaving one unique, page-specific description per URL.
2. Add JSON-LD to the kit and product pages (at minimum `Product` + `BreadcrumbList`; add `Offer` only if price/availability are truly present and maintained).
3. Improve the tutorials hub discoverability by adding an internal entry point to the planned tutorial slug `stm32-self-balancing-car-setup` and introducing a simple H2 structure for scanability.
