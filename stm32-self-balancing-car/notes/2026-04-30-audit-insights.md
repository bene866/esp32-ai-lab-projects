# SEO Audit — STM32 Self-Balancing Car Kit — 2026-04-30

## Crawl status (audit input)
The provided audit reports `200 OK` and `ok=true` for all audited URLs below.

## Page-level snapshot (audit input)
| URL | Title | Meta descriptions | Canonical | Headings | Images | Internal links | Schema (JSON-LD) |
|---|---|---:|---:|---|---:|---:|---:|
| `https://feigen8n.online/tutorials/` | `Tutorials – ESP32 AI Lab` | 1 | 1 | H1: `Tutorials`, H2: 0 | 0 | 21 | No |
| `https://feigen8n.online/kits/stm32-self-balancing-car-kit/` | `STM32 Self-Balancing Car Kit \| PID Control Robotics Project` | 2 | 1 | H1: `STM32 Self-Balancing Car Kit`, H2: 9 | 8 (missing alt: 0) | 21 | No |
| `https://feigen8n.online/product/stm32-self-balancing-car-kit/` | `STM32 Self-Balancing Car Kit \| PID Control Robotics Project` | 2 | 1 | H1: `STM32 Self-Balancing Car Kit`, H2: 9 | 8 (missing alt: 0) | 21 | No |

## Key risks (audit-based)
- Kit + product pages render duplicate meta description tags (`count=2`), which can confuse crawlers and produce inconsistent snippets.
- Kit + product pages share the same title and similar positioning, which can dilute intent separation.
- Tutorials hub is structurally thin in the audit (no H2, no images) and lacks JSON-LD.

## Prioritized actions (next edits)
1. Ensure each kit/product page outputs exactly one meta description tag (`meta_description_count=1`) and make the two descriptions distinct by intent.
2. Add JSON-LD to tutorials hub, kit page, and product page (all reported absent in the audit): at minimum `BreadcrumbList` (if breadcrumbs exist) and either `CollectionPage`/`ItemList` (tutorials hub) or `Product` (kit/product pages, using only listing-backed fields).
3. Add at least one meaningful H2 section to the tutorials hub and a small image block with alt text so the hub is not limited to one H1 and zero images in the audit.
