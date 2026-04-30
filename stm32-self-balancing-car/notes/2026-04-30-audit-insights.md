# SEO Audit Report — STM32 Self-Balancing Car Kit (2026-04-30)

## Scope
- Focus kit page: https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- Product page: https://feigen8n.online/product/stm32-self-balancing-car-kit/
- Tutorials index (related hub): https://feigen8n.online/tutorials/

## Crawl Status
- Tutorials index: `200 OK` (ok=true)
- Kit page: `200 OK` (ok=true)
- Product page: `200 OK` (ok=true)

## Titles & Meta Descriptions
- Tutorials index
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description: present, count=`1` (unique on-page)
- Kit page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present, count=`2` (duplicate meta description tags)
- Product page
  - Title: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Meta description: present, count=`2` (duplicate meta description tags)

## Canonical
- Tutorials index: canonical count=`1`
- Kit page: canonical count=`1`
- Product page: canonical count=`1`

## Headings
- Tutorials index
  - H1: `Tutorials` (1)
  - H2: none (count=`0`)
- Kit page
  - H1: `STM32 Self-Balancing Car Kit` (1)
  - H2: count=`9` (includes “Order This Kit”, “What You Can Explore”, “What’s Included”, “Key Features”, etc.)
- Product page
  - H1: `STM32 Self-Balancing Car Kit` (1)
  - H2: count=`9` (same structure as kit page)

## Images (Count + Alt)
- Tutorials index: images=`0` (alt issues not applicable)
- Kit page: images=`8`, missing alt=`0`
- Product page: images=`8`, missing alt=`0`

## Internal Links
- Tutorials index: internal links=`21` (includes navigation + multiple tutorial links)
- Kit page: internal links=`21` (includes nav + cart + add-to-cart/buy-now)
- Product page: internal links=`21` (includes nav + cart + add-to-cart/buy-now)

## Structured Data (Schema)
- Tutorials index: JSON-LD schema present? `false`
- Kit page: JSON-LD schema present? `false`
- Product page: JSON-LD schema present? `false`

## Prioritized Actions (Top 3)
1. Fix duplicate meta description tags on both the kit and product pages (meta_description_count=`2` each) so each page renders a single, consistent description in SERP snippets.
2. Add JSON-LD schema:
   - `Product` (kit/product pages) with name, offer price, availability, and image.
   - `CollectionPage` or `ItemList` (tutorials index) to describe the tutorial listing.
3. Create and interlink a dedicated tutorial page for the topic (`STM32 self-balancing car setup and PID calibration checklist`) and add contextual internal links:
   - From kit/product pages to the tutorial (setup + calibration guide).
   - From the tutorial back to the kit page (purchase/kit details) and optionally to `/tutorials/` as the hub.
