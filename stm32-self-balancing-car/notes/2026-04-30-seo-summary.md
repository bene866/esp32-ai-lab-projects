Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

## SEO snapshot (audit-based)
- Audited URLs (`200 OK`, `ok=true`):
  - Tutorials hub: `https://feigen8n.online/tutorials/`
  - Kit page: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - Product page: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Canonicals: `canonical_count=1` on all three pages (good baseline duplicate-control signal in this snapshot).
- Titles:
  - Tutorials hub: `Tutorials – ESP32 AI Lab`
  - Kit + Product: `STM32 Self-Balancing Car Kit | PID Control Robotics Project` (same title on both pages).
- Meta descriptions:
  - Tutorials hub: `meta_description_count=1` (excerpt appears truncated in the crawl snapshot).
  - Kit + Product: `meta_description_count=1` and the text matches between kit/product pages in the provided audit.
- Structure:
  - Tutorials hub: `h1=["Tutorials"]`, `h2_count=0`
  - Kit + Product: `h1=["STM32 Self-Balancing Car Kit"]`, `h2_count=11` including “Related setup guides” and the setup checklist title.
- Media/accessibility:
  - Tutorials hub: `image_count=0`
  - Kit + Product: `image_count=8`, `missing_alt_count=0` (good).
- Schema:
  - Tutorials hub: `has_schema_json_ld=false`
  - Kit + Product: `has_schema_json_ld=true`
- Internal linking:
  - Tutorials hub: `internal_link_count=23` and includes a visible link to `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`.
  - Kit + Product: `internal_link_count=22` and includes a “Related setup guides” section with the same tutorial.

## Generated files (today’s run)
- `audit-insights.md` — consolidated crawl-status + indexability signals limited to provided snapshot.
- `tutorial-draft.md` — checklist-style tutorial draft for `slug: stm32-self-balancing-car-setup` targeting setup bring-up + PID calibration readiness.
- `product-seo-review.md` — on-page SEO notes for kit/product pages (title/meta/H-structure/images/internal links) against the stated search intent.
- `internal-link-suggestions.md` — internal/external link plan emphasizing “setup + PID tuning” paths without over-promising exact kit revisions.
- `github-readme-update-draft.md` — README-oriented version of the same checklist intent for `repo_dir: stm32-self-balancing-car`.

## GitHub README intent (what the update is trying to achieve)
- Make the repository read like a **bring-up checklist**, not a “one true wiring diagram”, emphasizing verify-on-your-build checkpoints.
- Put the highest-failure-risk items up front: power/ground sanity, IMU axes/sign correctness, encoder direction/polarity, and motor direction mapping before any PID work.
- Keep commercial links secondary and clearly separated via a small “Related pages” style block (kit/product/tutorial).

## Risks / watch-outs (based on provided context)
- **Duplicate positioning between kit and product pages:** same title and same meta description in the audit snapshot can blur differentiation (especially if both rank for the same query intent).
- **Revision variability:** the tutorial and README must continue to avoid implying a fixed IMU model, fixed pinout, or guaranteed firmware flow (“pass/fail” verification language is the right tone).
- **Tutorial hub thin structure:** `h2_count=0` and no schema; it works as a directory, but offers limited topical context beyond the excerpted intro text.

## Next automated action (not executed)
- Prepare a PR-ready README update for the GitHub project by applying the structure from `github-readme-update-draft.md` into the `stm32-self-balancing-car` repository README, and cross-check that the “Related pages” URLs match:
  - Tutorial: `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
  - Kit: `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
  - Product: `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
