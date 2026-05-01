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
- Kit + Product pages show one H1 (“STM32 Self-Balancing Car Kit”) and `h2_count: 9` with sections including “What You Can Explore”, “What’s Included”, and “Shipping & Quote”.
- Kit + Product pages show `image_count: 8` and `missing_alt_count: 0`.
- Tutorials hub shows `has_schema_json_ld: false`, `image_count: 0`, `h1: Tutorials`, and `internal_link_count: 21`.

## Title and meta recommendations
- Differentiate intent (learning/checklist vs purchase) while keeping the product name.
  - Kit title option: “STM32 Self-Balancing Car Kit — Setup + PID Checklist (Verify Your Build)”
  - Product title option: “STM32 Self-Balancing Car Kit — Two-Wheel PID Learning Kit (Contents Vary)”
- Reduce to exactly one meta description per page (unique per URL).
  - Meta option (kit/tutorial intent): “A safety-first setup and PID tuning checklist for a two-wheel STM32 balancing car workflow. Verify your kit contents, wiring, and firmware before first power-on.”
  - Meta option (product intent): “STM32 self-balancing car kit for PID learning and experimentation. Check the product page for the current contents, compatibility notes, and documentation links.”

## H1/H2 guidance
- Keep the current H1 if it matches the product name.
- Add/position an H2 that mirrors the tutorial intent (for example, “Setup and PID Calibration Checklist”) to connect learning intent to action.
- Ensure “What’s Included” stays factual and revision-safe (avoid guarantees; point to packing list / current page revision).

## FAQ ideas (draft topics)
- “What should I validate before enabling balance PID?”
- “How do I confirm motor direction and encoder sign?”
- “How do I verify IMU axis orientation on my chassis?”
- “What’s a safe order for tuning P, D, then I?”
- “What optional modules (if any) are supported on my kit revision?”

## Schema recommendations
- Add JSON-LD `Product` + `BreadcrumbList`.
- Add `Offer` fields only if your page reliably displays and maintains price/currency/availability.
- Add `FAQPage` only after the Q&A is written and kept consistent with on-page instructions.

## Publishing risks to review
- Duplicate meta descriptions can create snippet instability; reduce to one per page.
- Kit and Product pages are structurally similar in crawl data; confirm unique purpose and avoid identical SEO fields across both.
- Avoid asserting pricing/stock/kit contents in metadata unless those details are explicitly present, maintained, and verified in the source content.
