Status: AI draft for review  
Focus project: Voice Quadruped Robot

# Daily SEO Summary — 2026-05-01

## SEO snapshot (audit-based)
- URLs checked (`200 OK`):  
  - `https://feigen8n.online/tutorials/`  
  - `https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/`  
  - `https://feigen8n.online/product/diy-voice-quadruped-robot-kit/`
- Titles:
  - Tutorials hub: `Tutorials – ESP32 AI Lab`
  - Kit + Product pages share the same title: `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo`
- Meta descriptions:
  - Tutorials hub: `count=1`
  - Kit page: `count=2` (duplicate meta description tags)
  - Product page: `count=2` (duplicate meta description tags)
- Canonical tags: all pages `count=1`
- Headings:
  - Tutorials hub: `H1=Tutorials`, `H2 count=0`
  - Kit page: `H1=DIY Voice-Controlled Quadruped Robot Kit`, `H2 count=10`
  - Product page: `H1=DIY Voice-Controlled Quadruped Robot Kit`, `H2 count=10`
- Images:
  - Tutorials hub: `0`
  - Kit page: `9` (`missing_alt_count=0`)
  - Product page: `9` (`missing_alt_count=0`)
- Internal links: `21` on each audited page (per provided samples)
- JSON-LD schema: not found on all three pages (`has_schema_json_ld=false`)

## Key issues to fix (site-side)
- Duplicate meta description tags on both kit and product pages (`meta_description_count=2`).
- Kit and product pages use identical page titles (harder to differentiate in search results).
- No JSON-LD detected on the tutorials hub or the two product surfaces.

## Generated files (today)
- `audit-insights.md` — audit recap for the three URLs
- `tutorial-draft.md` — WordPress draft: `voice-quadruped-robot-assembly-guide` (assembly + first movement checks; avoids unverified wiring/commands)
- `product-seo-review.md` — applied-now recommendations list (not executed)
- `internal-link-suggestions.md` — where to link the kit/product pages to the planned tutorial URL
- `github-readme-update-draft.md` — repo-facing README draft for the quadruped robot documentation

## GitHub README intent (repo draft)
- Positions the project as a documentation home for assembly notes + bring-up checklist + repeatable movement observations.
- Explicitly marks validation as “draft for human review” and keeps placeholders for kit-revision specifics (media, wiring labels, board details).

## Risks / unknowns (must stay review-gated)
- Assembly/wiring/voice-command specifics are not present in today’s audit context, so the tutorial and README must remain checklist-oriented until verified against the exact kit revision.
- The tutorial URL `/tutorials/voice-quadruped-robot-assembly-guide/` should not be linked from the store pages until it is live.

## Next automated action (queued)
- After the tutorial slug is published: apply the internal-link placements from `internal-link-suggestions.md` on both the kit and product pages, then re-run the same 3-URL audit to confirm (1) the tutorial link appears, and (2) `meta_description_count` is no longer duplicated on kit/product pages.
