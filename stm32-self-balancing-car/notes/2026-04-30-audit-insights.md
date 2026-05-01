# SEO Audit Report — STM32 Self-Balancing Car Kit — 2026-04-30

## Scope and inputs
This report uses the provided audit JSON for three URLs and the focus project brief for “STM32 self-balancing car setup and PID calibration checklist.” The audited URLs are:
- `https://feigen8n.online/tutorials/`
- `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Crawl status and indexability signals
All three audited pages returned `200 OK` with `ok=true`, which indicates they are reachable by a crawler and not blocked by an obvious server-side error. Each page shows `canonical_count: 1`, which is a positive indexability signal because it suggests a single canonical URL is declared per page. The audit does not include robots directives, sitemap coverage, or `noindex` checks, so those aspects cannot be verified from the provided context.

## Title and meta description
- Tutorials hub (`/tutorials/`):
  - Title: “Tutorials – ESP32 AI Lab”
  - Meta description count: `1`
  - The meta description excerpt is truncated in the audit output, which suggests it may be long or auto-generated, but its full length cannot be confirmed here.
- Kit and product pages:
  - Both pages share the same title: “STM32 Self-Balancing Car Kit | PID Control Robotics Project.”
  - Both pages share the same meta description text about a DIY STM32 self-balancing car kit with PID, IMU, encoder feedback, and app control.
  - Having identical title and meta description across two separate URLs can reduce SERP differentiation and may weaken click-through performance when both pages are eligible to rank.

## Headings and page structure
- Tutorials hub:
  - H1: “Tutorials”
  - H2 count: `0`
  - The page excerpt shows a list of guides (including the STM32 self-balancing car checklist), but the lack of H2 sections can reduce scannability and limit keyword-relevant subtopics on the hub page.
- Kit and product pages:
  - H1: “STM32 Self-Balancing Car Kit”
  - H2 count: `11`
  - H2 samples include “Related setup guides” and “STM32 self-balancing car setup and PID calibration checklist,” which aligns well with the stated search intent for setup, IMU checks, motor direction, and PID tuning.

## Content depth and intent match
The kit/product excerpts describe a hands-on learning kit centered on PID control, IMU attitude sensing, encoder motor feedback, and embedded robotics experiments. The “Related setup guides” section introduces the checklist-style tutorial and includes an explicit caution that kit contents and firmware vary by seller and revision, which is helpful for safety and expectation-setting. The excerpt indicates a “Read setup guide” call to action exists, but the audit does not include a crawl of the tutorial page itself, so the tutorial’s on-page completeness, keyword coverage, and indexability cannot be confirmed from the provided data.

The tutorials hub excerpt includes multiple guide titles and a short statement that the guides focus on wiring checks, setup flow, validation steps, and safe next actions. The hub page has `image_count: 0`, which can be acceptable for a directory page, but it may limit visual engagement and reduce opportunities for image-based internal linking if thumbnails are desired.

## Images and alt text
- Tutorials hub: `image_count: 0`, `missing_alt_count: 0`.
- Kit and product pages: `image_count: 8`, `missing_alt_count: 0`.
The kit/product pages appear to have consistent alt coverage (no missing alt attributes reported), which is a positive accessibility and image SEO signal. The audit does not include the actual alt text strings, so relevance and descriptiveness cannot be assessed here.

## Internal linking and anchor text
- Tutorials hub: `internal_link_count: 23`, with samples that include navigation links and a direct link to `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/` using the anchor “STM32 self-balancing car setup and PID calibration checklist.”
- Kit and product pages: `internal_link_count: 22`, with samples including navigation links and prominent conversion links (Add to Cart and Buy Now).
The presence of a clearly worded, intent-aligned tutorial anchor on the tutorials hub is a strength because it matches the project topic and provides a direct path into the checklist content.

## External authority references
The provided internal link samples do not show external authority references. If the kit/product pages and the tutorial currently contain few or no outbound citations, adding a small number of relevant official references can strengthen perceived credibility for setup and tooling topics. The focus brief lists two suitable official references:
- STM32Cube documentation (STM32CubeIDE)
- ST motor control ecosystem resources

## Structured data (schema)
- Tutorials hub: `has_schema_json_ld: false`.
- Kit and product pages: `has_schema_json_ld: true`.
This suggests structured data is present on commerce pages, but absent on the tutorials directory. The audit does not specify the schema type on the kit/product pages, so it cannot be evaluated for completeness or correctness here.

## Conversion path and commercial clarity
Both the kit and product pages include visible purchase CTAs with `?add-to-cart=122&quantity=1` and a “Buy Now” variant, and the excerpt states the item is “In stock.” The excerpt also shows a launch sale price (`$99.00`) and regular price (`$129.00`), which supports purchase intent. The “Related setup guides” block adds a pre-purchase and post-purchase support path by directing readers to the setup checklist, which can reduce returns and improve buyer confidence if the tutorial content is thorough.

## 5 prioritized actions (highest impact first)
1. Differentiate the kit vs product page titles and meta descriptions so each URL targets a distinct intent and avoids duplicate SERP snippets.  
2. Add JSON-LD to the tutorials hub (for example, a tutorial list structure) so the directory page communicates its content type and inventory more clearly.  
3. Add H2 sections to `/tutorials/` to group guides by theme (for example, STM32 robotics, ESP32 dashboards, voice control) and to increase scannability beyond a flat list.  
4. Ensure strong bidirectional internal linking among the kit page, product page, and the STM32 setup checklist page using intent-specific anchors (setup, IMU checks, motor direction, PID tuning).  
5. Add 1–2 official external references on the STM32 setup checklist (and optionally on kit/product pages) using the provided STM32CubeIDE and ST motor control resources to strengthen authority for tooling and control-system guidance.
