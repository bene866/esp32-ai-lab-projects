Status: AI draft for review  
Focus project: STM32 Self-Balancing Car Kit

# Daily SEO Summary — 2026-04-30

## SEO status (from provided audit)
Audited URLs (all reachable at audit time):
- https://feigen8n.online/tutorials/ → `200 OK`, `ok=true`, `canonical_count=1`, `has_schema_json_ld=false`
- https://feigen8n.online/kits/stm32-self-balancing-car-kit/ → `200 OK`, `ok=true`, `canonical_count=1`, `has_schema_json_ld=true`
- https://feigen8n.online/product/stm32-self-balancing-car-kit/ → `200 OK`, `ok=true`, `canonical_count=1`, `has_schema_json_ld=true`

Notable on-page signals:
- Tutorials hub: H1 = “Tutorials”, `h2_count=0`, `image_count=0`, 23 internal links (includes the STM32 tutorial entry). Meta description exists (`meta_description_count=1`) but appears long/truncated in the excerpt.
- Kit + Product pages: same title and same meta description (both have `meta_description_count=1`), H1 matches product name, 8 images with `0` missing `alt`, strong section structure (`h2_count=11`).

Indexing unknowns (not present in the audit input): robots directives, `noindex`, sitemap coverage, and redirect chains.

## Generated files (draft outputs)
- `audit-insights.md` — audit recap and gaps (what was/wasn’t measured).
- `tutorial-draft.md` — WordPress-targeted checklist tutorial draft for `/tutorials/stm32-self-balancing-car-setup/` aligned to “STM32 self balancing car kit”, “self balancing robot PID tuning”, “IMU robot car setup”.
- `product-seo-review.md` — page-level SEO notes for kit + product pages vs. setup intent.
- `internal-link-suggestions.md` — internal linking plan between Tutorials hub ↔ tutorial ↔ kit/product pages.
- `github-readme-update-draft.md` — README-style bring-up + tuning checklist text for the GitHub repo documentation.

## GitHub README intent (documentation-only)
The README draft is positioned as a build-specific validation checklist to reduce “PID guessing” by insisting on observable confirmations first (IMU plausibility/axes, motor direction symmetry, encoder sign, loop timing/power stability). It explicitly avoids assuming a single PCB/firmware revision and frames every step as “pass only if you can verify it on your hardware”.

## Risks / opportunities
- Duplicate SERP snippet risk: kit + product pages currently share the same title and meta description.
- Tutorials hub may under-serve search and UX: long meta description excerpt, no H2 structure, and no images (even a small visual index could help scanning).
- Indexing controls can’t be confirmed from the audit dataset (robots/noindex/sitemap/redirects not checked).
- Tutorial success depends on including the “pre-tuning” checks prominently (IMU axis mapping + motor/encoder sign) to match the stated setup/tuning intent.

## Next automated action (do not publish)
1) Convert `github-readme-update-draft.md` into the target repo’s README within `repo_dir: stm32-self-balancing-car` as a review-only doc change (no claims of verified hardware results).  
2) Apply the highest-value internal links from `internal-link-suggestions.md` (Tutorials hub → tutorial; kit/product → tutorial; tutorial → kit/product).  
3) Propose differentiating the kit vs. product page titles/meta descriptions (same intent, different page type) while keeping canonicals intact.
