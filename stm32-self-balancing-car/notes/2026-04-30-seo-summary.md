Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

## SEO snapshot (audit-based)
- URLs checked (`200 OK`):  
  - `https://feigen8n.online/tutorials/`  
  - `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`  
  - `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- Titles:
  - Tutorials hub: `Tutorials – ESP32 AI Lab`
  - Kit page: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
  - Product page: `STM32 Self-Balancing Car Kit | PID Control Robotics Project`
- Meta descriptions:
  - Tutorials hub: present (`count=1`)
  - Kit page: duplicated (`count=2`)
  - Product page: duplicated (`count=2`)
- Canonicals: present on all three pages (`count=1`)
- Headings & content structure:
  - Tutorials hub: H1=`Tutorials`, no H2 (`h2_count=0`), no images (`image_count=0`)
  - Kit/Product pages: H1 present; H2 count=`9` (includes sections like ordering, included parts, features, gallery, notes, shipping)
- Structured data: Schema JSON-LD not detected on all three pages

## Generated files (today)
- `audit-insights.md` — crawl findings and issues (meta duplication, missing schema, hub page structure)
- `tutorial-draft.md` — `stm32-self-balancing-car-setup` checklist draft (setup order + safe PID calibration workflow; no assumed gains)
- `product-seo-review.md` — audit summary + concrete on-page SEO recommendations (not applied)
- `internal-link-suggestions.md` — 2 link placements from kit/product pages to `/tutorials/stm32-self-balancing-car-setup/`
- `github-readme-update-draft.md` — review-required README draft framing (firmware + tuning notes as checklists, not “verified results”)

## GitHub README intent (repo: `stm32-self-balancing-car`)
- Provide a checklist-first onboarding doc: bench-safe bring-up, polarity/sign sanity checks (IMU + encoders + motors), and a staged PID tuning workflow.
- Keep all behavior statements as diagnostic targets; explicitly avoid claiming real-world balance success.

## Risks / blockers to address
- Duplicate meta descriptions on kit and product pages (`meta_description_count=2`) can dilute snippets and reduce consistency.
- No JSON-LD detected (site-wide across the audited pages), limiting rich-result eligibility signals.
- Tutorial hub is thin structurally (no H2, no images), making internal discovery/navigation weaker.
- Tuning content must remain “review-required” and avoid any implied validated PID values or confirmed hardware performance.

## Next automated action (queued)
- Prepare the tutorial landing URL `/tutorials/stm32-self-balancing-car-setup/` as a draft (matching the checklist positioning) and stage the two internal links from kit/product pages using the suggested anchors.
- Create a PR-ready README update from `github-readme-update-draft.md` into the `stm32-self-balancing-car` repo directory after a human confirms filenames/paths and any referenced materials exist.
