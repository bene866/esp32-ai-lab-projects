# SEO Audit Report — STM32 Self-Balancing Car Kit — 2026-04-30

## Scope (URLs audited)
- Tutorials hub: `https://feigen8n.online/tutorials/`
- Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`

## Crawlability & indexability
All three audited URLs returned a successful HTML response with `status=200` and `ok=true`, which means they are reachable for crawlers at the time of the audit. Each audited page reports `canonical_count=1`, which is a positive signal for consolidating indexing to a preferred URL. The audit input does not include robots directives, noindex tags, sitemap references, or redirect chains, so those indexability factors cannot be confirmed in this report.

## Title tags & meta descriptions
The tutorials hub uses the title “Tutorials – ESP32 AI Lab” and has exactly one meta description (`meta_description_count=1`). The meta description text appears truncated in the audit excerpt, which suggests it may be longer than ideal for search snippets even though it is present. Both the kit page and the product page use the same title, “STM32 Self-Balancing Car Kit | PID Control Robotics Project,” and both pages also use the same meta description text describing PID control, IMU sensing, encoder feedback, and app control (`meta_description_count=1` on each). Identical titles and identical meta descriptions across two indexable pages increase the risk of duplicate snippet behavior and unclear page intent in search results, even if both pages are valid and useful.

## Headings & on-page structure
The tutorials hub has a single H1 (“Tutorials”) and reports `h2_count=0`, which means there are no H2 subtopics to help organize the page for scanning users and search engines. The kit page has an H1 (“STM32 Self-Balancing Car Kit”) and a strong subheading structure with `h2_count=11`, including sections like “Related setup guides,” “What You Can Explore,” “What’s Included,” “Key Features,” and “Shipping & Quote.” The product page mirrors the kit page with the same H1 and the same H2 count (`h2_count=11`), which supports readability but also reinforces that the two pages are structurally very similar.

## Content depth & intent match
The tutorials hub excerpt indicates it functions as a directory for multiple guides, including the specific STM32 checklist tutorial (“STM32 self-balancing car setup and PID calibration checklist”). The kit and product page excerpts contain both commercial and educational content, including “Order This Kit,” pricing context (regular price and launch price wording), “In stock,” and a “Related setup guides” block that explains the checklist-style setup approach and warns that kit revisions vary. This mixed content supports the stated search intent (“setup, IMU checks, motor direction, PID tuning checklist”) because it provides a next step for learners instead of stopping at a purchase prompt.

## Images & alt text
The tutorials hub reports `image_count=0`, which means it has no images to carry visual affordances, preview cues, or image search entry points. The kit page reports `image_count=8` and the product page reports `image_count=8`, and both pages report `missing_alt_count=0`, which indicates alt text coverage is complete for the images that exist. The audit does not include image file sizes or performance metrics, so the impact of images on page speed cannot be evaluated here.

## Internal linking & navigation
Internal navigation is present across the audited pages, including links to core sections such as Home, Kits, Projects, About, Contact/Inquiry, Tutorials, and Cart. The tutorials hub reports `internal_link_count=23` and includes a direct link to `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/` with the anchor “STM32 self-balancing car setup and PID calibration checklist.” The kit and product pages report `internal_link_count=22` each and include transactional links such as “Add to Cart” and “Buy Now,” plus a “Related setup guides” section that routes users to the setup checklist. This creates a reasonable loop between discovery (tutorial index), education (tutorial), and conversion (kit/product), but the tutorial index page currently lacks subheadings that could make those pathways more explicit.

## External authority references (trust signals)
The focus project includes two official references that can be used as authority links where appropriate: “STM32Cube documentation” (`https://www.st.com/en/development-tools/stm32cubeide.html`) and “ST motor control resources” (`https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html`). The audit excerpt does not show these external links present on the audited pages, so their current on-page usage cannot be confirmed from the provided data. If added thoughtfully, these references can support credibility for setup and motor-control concepts without changing the product positioning.

## Structured data (schema)
The tutorials hub reports `has_schema_json_ld=false`, so it does not currently expose JSON-LD according to the audit input. The kit page and product page both report `has_schema_json_ld=true`, which is a positive baseline for ecommerce-style rich results. The audit does not specify schema types or properties, so completeness and validity cannot be confirmed within this report.

## Conversion path & ecommerce UX signals
Both the kit and product pages contain clear conversion CTAs, including “Add to Cart,” “Buy Now,” and “Ask a Question,” and they also link to Cart in the global navigation. The excerpt also includes “Shipping options may vary by destination,” a “Shipping & Quote” section heading, and a “Notes / Disclaimer” heading, which supports purchase readiness by addressing common buyer concerns. The tutorials hub includes a Cart link, but it does not include images or H2 groupings that could help route users from learning intent to the most relevant kit pages faster.

## 5 prioritized actions (highest impact first)
1. Differentiate the kit and product page titles and meta descriptions so each page has a distinct search intent and snippet, while keeping the primary keywords aligned to “STM32 self balancing car kit,” “self balancing robot PID tuning,” and “IMU robot car setup.”
2. Add JSON-LD to the tutorials hub (`has_schema_json_ld=false`) so the page better represents a tutorial collection and improves eligibility for enhanced presentation, while keeping the implementation consistent with the site’s existing schema patterns.
3. Introduce a small H2 structure on the tutorials hub (`h2_count=0`) to group tutorials by topic (for example STM32 robotics vs ESP32 smart home) and to surface the STM32 balancing checklist link more prominently.
4. Add at least one relevant visual element to the tutorials hub (`image_count=0`) to increase scannability and engagement, while maintaining the current standard of complete alt text on all images (`missing_alt_count=0` is already achieved elsewhere).
5. Add or verify a short “Official references” block on the STM32 setup tutorial (and optionally on kit/product pages) that links to STM32Cube IDE documentation and ST motor control ecosystem pages, because these are the provided authoritative references for toolchain and motor-control context.
