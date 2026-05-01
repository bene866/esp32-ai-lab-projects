# SEO Audit Report — STM32 Self-Balancing Car Kit — 2026-04-30

## Scope (provided crawl)
- `https://feigen8n.online/tutorials/`
- `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Crawl status
- All URLs: `200 OK` (`ok=true`)

## Titles & meta descriptions
- Tutorials hub
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description: present (`meta_description_count=1`)
  - Canonical: present (`canonical_count=1`)
- Kit page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present but duplicated (`meta_description_count=2`)
  - Canonical: present (`canonical_count=1`)
- Product page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present but duplicated (`meta_description_count=2`)
  - Canonical: present (`canonical_count=1`)

## Headings
- Tutorials hub: `h1=["Tutorials"]`, `h2_count=0`
- Kit page: `h1=["STM32 Self-Balancing Car Kit"]`, `h2_count=9` (e.g., Order / Included / Features / Gallery / Shipping)
- Product page: `h1=["STM32 Self-Balancing Car Kit"]`, `h2_count=9` (same structure as kit page)

## Images
- Tutorials hub: `image_count=0`
- Kit page: `image_count=8`, `missing_alt_count=0`
- Product page: `image_count=8`, `missing_alt_count=0`

## Internal links
- All pages: `internal_link_count=21`
- Tutorials hub internal link samples include `/tutorials/xiaozhi-compatible-esp32-voice-assistant/`, `/tutorials/esp32-s3-camera-ai-vision-starter/`, `/tutorials/esp32-smart-home-voice-control/`, `/tutorials/esp32-sensor-dashboard/`
- Kit/Product page samples include add-to-cart and site navigation links (Home/Kits/Projects/About/Contact/Tutorials/Cart)

## Schema (JSON-LD)
- Tutorials hub: `has_schema_json_ld=false`
- Kit page: `has_schema_json_ld=false`
- Product page: `has_schema_json_ld=false`

## Prioritized actions (next 3)
1) **Fix duplicated meta description tags** on the kit and product pages (`meta_description_count=2`) so each page outputs exactly one meta description.  
2) **Add JSON-LD schema**:
   - Product/Offer schema for the product page (and optionally the kit page if it is also a purchase landing page)
   - CollectionPage/ItemList (or equivalent) for the tutorials hub  
3) **Improve tutorials hub structure and discoverability**:
   - Add 1–3 meaningful H2 sections (currently `h2_count=0`)
   - Consider adding at least one representative image per tutorial block (currently `image_count=0`) while keeping alt coverage consistent with other pages (`missing_alt_count=0`)
   - Once the planned tutorial exists, add a clear internal route to `/tutorials/stm32-self-balancing-car-setup/` from the STM32 kit/product pages and the tutorials hub.
