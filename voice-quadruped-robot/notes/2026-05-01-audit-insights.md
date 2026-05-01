# SEO Audit Report — 2026-05-01 — Voice Quadruped Robot

## Crawl status (provided audit)
- `https://feigen8n.online/tutorials/` returned `200` with `ok=true`.
- `https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/` returned `200` with `ok=true`.
- `https://feigen8n.online/product/diy-voice-quadruped-robot-kit/` returned `200` with `ok=true`.

## Titles and meta descriptions
- Tutorials hub title is `Tutorials – ESP32 AI Lab` with `meta_description_count=1`, and the description states it is “English build guides for practical ESP32 projects…”.
- Kit page title is `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo` with `meta_description_count=2`.
- Product page title is `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo` with `meta_description_count=2`.
- All audited pages report `canonical_count=1`.

## Headings
- Tutorials hub has H1 `Tutorials`, and `h2_count=0`.
- Kit page H1 is `DIY Voice-Controlled Quadruped Robot Kit`, and it reports `h2_count=10` with samples including `What You Can Explore`, `What’s Included`, and `Key Features`.
- Product page matches the kit page for H1 and reports `h2_count=10` with the same sampled section names.

## Images
- Tutorials hub has `image_count=0`.
- Kit page has `image_count=9` with `missing_alt_count=0`.
- Product page has `image_count=9` with `missing_alt_count=0`.

## Internal links
- Tutorials hub reports `internal_link_count=21`, including navigation links and multiple tutorial links such as `/tutorials/xiaozhi-compatible-esp32-voice-assistant/` and `/tutorials/esp32-s3-camera-ai-vision-starter/`.
- Kit and product pages each report `internal_link_count=21`, and the sample includes navigation links plus purchase links such as `?add-to-cart=121&quantity=1` and `...&espai_buy_now=1`.

## Schema (JSON-LD)
- All audited pages report `has_schema_json_ld=false`.

## Prioritized actions (next changes)
1. Reduce `meta_description_count` from `2` to `1` on both the kit page and the product page, and make each remaining description unique to its page intent.
2. Add JSON-LD to the kit and product pages, because the audit reports no schema on any audited URL, and product-oriented structured data can be validated after publishing.
3. Expand the Tutorials hub information architecture by adding at least two H2 sections and linking the new tutorial target `/tutorials/voice-quadruped-robot-assembly-guide/` from the kit page section `What You Can Explore` to connect “learn” traffic to a single assembly and movement test guide.
