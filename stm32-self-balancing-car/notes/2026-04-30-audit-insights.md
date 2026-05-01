# SEO Audit Report — STM32 Self-Balancing Car Kit (2026-04-30)

## Scope (provided crawl)
- `https://feigen8n.online/tutorials/`
- `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Crawl status
- All 3 URLs: `200 OK` (`ok=true`)

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

## Canonicals
- All 3 URLs: canonical present (`canonical_count=1`)

## Headings
- Tutorials hub
  - H1: `Tutorials`
  - H2: none (`h2_count=0`)
- Kit page
  - H1: `STM32 Self-Balancing Car Kit`
  - H2: 9 (includes: `Order This Kit`, `What You Can Explore`, `What’s Included`, `Key Features`, `Product Photo`, `Gallery`, `Notes / Disclaimer`, `Shipping & Quote`, `Need a different version?`)
- Product page
  - H1: `STM32 Self-Balancing Car Kit`
  - H2: 9 (same set as kit page)

## Images (and alt coverage)
- Tutorials hub
  - Images: 0
  - Missing alt: 0
- Kit page
  - Images: 8
  - Missing alt: 0
- Product page
  - Images: 8
  - Missing alt: 0

## Internal links (count + sample anchors)
- Tutorials hub: 21 internal links (includes nav + tutorial entries like `XiaoZhi-Compatible ESP32 Voice Assistant Starter Guide`, `ESP32-S3 Camera AI Vision Starter Guide`)
- Kit page: 21 internal links (includes `Tutorials`, `Cart`, and repeated `Add to Cart` / `Buy Now`)
- Product page: 21 internal links (includes `Tutorials`, `Cart`, and repeated `Add to Cart` / `Buy Now`)

## Structured data (JSON-LD)
- All 3 URLs: no JSON-LD detected (`has_schema_json_ld=false`)

## 3 prioritized actions
1) **Fix duplicated meta descriptions on kit + product pages** (`meta_description_count=2` on both) to ensure only one meta description is output per page.  
2) **Add JSON-LD**: `Product` schema for the kit/product pages and a suitable listing schema for the tutorials hub (currently none detected on any URL).  
3) **Improve the Tutorials hub content structure** by adding meaningful H2 sections (currently `h2_count=0`) and, if appropriate, adding at least one image block (currently `image_count=0`) while keeping alt text coverage consistent with the kit/product pages.
