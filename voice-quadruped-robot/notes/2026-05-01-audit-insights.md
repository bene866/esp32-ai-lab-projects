# SEO Audit Report — Voice Quadruped Robot (2026-05-01)

## Scope (provided crawl)
- Tutorials index: `https://feigen8n.online/tutorials/`
- Kit page: `https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/`
- Product page: `https://feigen8n.online/product/diy-voice-quadruped-robot-kit/`

## Crawl status
- All three URLs returned `200 OK` (`ok=true`).

## Titles & meta descriptions
- Tutorials index
  - Title: `Tutorials – ESP32 AI Lab`
  - Meta description count: `1`
- Kit page
  - Title: `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo`
  - Meta description count: `2` (duplicate meta description tags)
- Product page
  - Title: `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo` (same as kit page)
  - Meta description count: `2` (duplicate meta description tags)
- Canonicals
  - All pages: canonical tag count `1`

## Headings
- Tutorials index
  - H1: `Tutorials`
  - H2 count: `0`
- Kit page
  - H1: `DIY Voice-Controlled Quadruped Robot Kit`
  - H2 count: `10` (includes “What You Can Explore”, “What’s Included”, “Key Features”, “Notes / Disclaimer”, etc.)
- Product page
  - H1: `DIY Voice-Controlled Quadruped Robot Kit`
  - H2 count: `10` (same section set as kit page)

## Images
- Tutorials index: `0` images
- Kit page: `9` images, missing alt count: `0`
- Product page: `9` images, missing alt count: `0`

## Internal links
- Tutorials index: `21` internal links (includes links to multiple tutorials and main nav items)
- Kit page: `21` internal links (includes nav + cart + purchase CTAs)
- Product page: `21` internal links (includes nav + cart + purchase CTAs)

## Structured data (Schema / JSON-LD)
- All pages: `has_schema_json_ld=false`

## Prioritized actions (next edits)
1. **Fix duplicate meta descriptions** on the kit and product pages (both report `meta_description_count: 2`) and ensure each page has a single, page-specific meta description.
2. **Differentiate kit vs product page SEO**: the kit and product pages currently share the same title; update to distinct, intent-matched titles (kit/assembly intent vs product/purchase intent) while keeping one canonical each.
3. **Add JSON-LD + strengthen tutorial routing**
   - Add JSON-LD (e.g., `Product` on product/kit pages; `CollectionPage` on tutorials index).
   - Add an internal link from the kit/product pages to the planned tutorial slug: `/tutorials/voice-quadruped-robot-assembly-guide/`, and add the tutorial to the tutorials hub once published.
