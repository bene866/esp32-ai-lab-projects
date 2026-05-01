# Product SEO Review — STM32 Self-Balancing Car Kit — 2026-04-30
Uniqueness seed: `3ea75862e301ff8f17e2ff046799322b24764393ccc4f248615753749725c0c3`  
Scope URLs:  
- Kit: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`  
- Product: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`  
- Tutorials hub: `https://feigen8n.online/tutorials/`

## Current-page observations (audit-based)
- All three URLs returned `200 OK` and were marked `ok=true`.
- Kit + Product pages share the same title: “STM32 Self-Balancing Car Kit | PID Control Robotics Project”.
- Kit + Product pages each show `meta_description_count: 2`, `canonical_count: 1`, and `has_schema_json_ld: false`.
- Kit + Product pages have one H1 (“STM32 Self-Balancing Car Kit”) and `h2_count: 9` with sections like “Order This Kit”, “What You Can Explore”, “What’s Included”, and “Shipping & Quote”.
- Kit + Product pages show `image_count: 8` and `missing_alt_count: 0`.
- Tutorials hub shows `has_schema_json_ld: false`, `image_count: 0`, `h1: Tutorials`, and `internal_link_count: 21`.

## Title and meta recommendations
- Keep one primary title per page and differentiate Kit vs Product intent.
  - Kit title option: “STM32 Self-Balancing Car Kit — Setup + PID Tuning Checklist”
  - Product title option: “STM32 Self-Balancing Car Kit — IMU + Encoder PID Robot Kit”
- Reduce to exactly one meta description per page.
  - Meta description option (general): “Build a two-wheel STM32 self-balancing robot and learn PID control with IMU attitude sensing, encoder motor feedback, app control support, and an ultrasonic module.”

## H1/H2 guidance
- Keep the current H1 as-is, because it matches the product name.
- Add an H2 that directly matches the intended tutorial topic, such as “Setup and PID Calibration Checklist”, and place it near “What You Can Explore” to connect learning intent to action.
- Consider merging or reordering H2s so that “What’s Included” appears before “Key Features” for faster scanning.

## FAQ ideas (draft topics)
- “What should I calibrate first: IMU, motors, or PID gains?”
- “How do encoder motors help balance control?”
- “What does the ultrasonic module do in obstacle avoidance or following mode?”
- “Is app control required for first power-on tests?”
- “What is included in the kit, and what is not included?”

## Schema recommendations
- Add JSON-LD `Product` schema (with `Offer`) to reflect the listed pricing and “In stock” status shown on the page excerpt.
- Add JSON-LD `FAQPage` for the tuning and setup questions above.
- Add JSON-LD `BreadcrumbList` on Kit and Product pages and on the Tutorials hub.

## Publishing risks to review
- Duplicate meta descriptions (`meta_description_count: 2`) can create snippet instability and should be reduced to one.
- Kit and Product pages appear highly similar in crawl data, so confirm unique page purpose and avoid identical SEO fields across both.
- No JSON-LD is present on audited pages, which can limit rich results even when content is strong.
- Avoid hardcoding promotional pricing in metadata if it may change, and keep pricing primarily in-page where updates are safer.
