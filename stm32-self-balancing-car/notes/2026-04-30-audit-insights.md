# SEO Audit — STM32 Self-Balancing Car Kit — 2026-04-30

## Crawl status (provided audit)
All audited URLs returned `200` with `ok=true`.

## Page-level snapshot
| URL | Title | Meta description | Canonical | Headings | Images | Internal links | Schema (JSON-LD) |
|---|---|---:|---:|---|---:|---:|---:|
| `https://feigen8n.online/tutorials/` | `Tutorials – ESP32 AI Lab` | 1 | 1 | H1: `Tutorials`, H2: 0 | 0 | 21 | No |
| `https://feigen8n.online/kits/stm32-self-balancing-car-kit/` | `STM32 Self-Balancing Car Kit \| PID Control Robotics Project` | 2 | 1 | H1: `STM32 Self-Balancing Car Kit`, H2: 9 | 8 (missing alt: 0) | 21 | No |
| `https://feigen8n.online/product/stm32-self-balancing-car-kit/` | `STM32 Self-Balancing Car Kit \| PID Control Robotics Project` | 2 | 1 | H1: `STM32 Self-Balancing Car Kit`, H2: 9 | 8 (missing alt: 0) | 21 | No |

## Titles & meta (observations)
- The kit page and product page share the same title and the same meta description text in the audit.
- The kit page and product page each show `meta_description_count=2`, which indicates duplicated meta description output.
- The tutorials hub has exactly one meta description and one canonical tag in the audit.

## Headings, images, and links (observations)
- The tutorials hub has one H1, no H2 sections, and no images in the audit.
- The kit and product pages use multiple H2 sections (9), include 8 images each, and show `missing_alt_count=0`.
- The audited internal link samples include repeated commerce anchors such as `Add to Cart` and `Buy Now` on the kit/product pages.

## Prioritized actions (next edits)
1. Remove the duplicate meta description output on the kit and product pages so each page renders exactly one meta description tag (`meta_description_count=1`).
2. Add JSON-LD to the tutorials hub, kit page, and product page because all three currently report `has_schema_json_ld=false`.
3. Improve the tutorials hub structure by adding at least one H2 section and a small image block (with alt text) so the page is not limited to a single H1 and zero images in the audit.
