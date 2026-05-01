# Product SEO Review — DIY Voice-Controlled Quadruped Robot Kit — 2026-05-01

Status: draft recommendations (not applied)  
Uniqueness seed: `816120a9df9c9b9da5a4fccd803294bb947c1f8b87c89543089850444d688afd`  
Focus: **Voice quadruped robot assembly and movement test guide** (planned tutorial slug: `voice-quadruped-robot-assembly-guide`)

## Pages reviewed (from provided audit)
- Tutorials hub: https://feigen8n.online/tutorials/ (`200 OK`)
- Kit page: https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/ (`200 OK`)
- Product page: https://feigen8n.online/product/diy-voice-quadruped-robot-kit/ (`200 OK`)

---

## Audit snapshot (current state)
### Tutorials hub (`/tutorials/`)
- Title: `Tutorials – ESP32 AI Lab`
- Meta description: present (`count=1`)
- Canonical: present (`count=1`)
- Headings: `H1=Tutorials`, `H2 count=0`
- Images: `0`
- Internal links: `21`
- JSON-LD schema: **not found**

### Kit + Product pages (both)
- Title: `DIY Voice-Controlled Quadruped Robot Kit | STEM Robotics Demo` (same on both)
- Meta description: present but **duplicated** (`count=2` on both)
- Canonical: present (`count=1` on both)
- H1: `DIY Voice-Controlled Quadruped Robot Kit` (present on both)
- H2 count: `10` (sample includes: Order / What You Can Explore / What’s Included / Key Features / Product Photo / Watch the assembly and movement demo / Gallery / Notes / Shipping / Need a different version?)
- Images: `9` with `0` missing alt (good)
- Internal links: `21`
- JSON-LD schema: **not found**

---

## Priority issues (SEO + UX)
1) **Duplicate meta descriptions (count=2)** on both kit and product pages  
- Likely reduces snippet control and can confuse crawlers. Goal: **exactly one** meta description tag per page.

2) **Kit and product pages share the same title**  
- Two different URLs competing for the same query set; weaker CTR testing and less clear intent separation.

3) **No JSON-LD schema detected** (tutorial hub + kit + product)  
- Missed chance for rich results (Product/FAQ/Video/Breadcrumbs) and clearer page type signals.

4) **Repetition risk around the demo section**  
- The excerpt shows “Watch the assembly and movement demo” repeated in close proximity; tighten copy so headings and body don’t echo the same line.

---

## Title recommendations (differentiate intent)
Keep titles distinct so each URL has a job.

### Kit page (`/kits/diy-voice-quadruped-robot-kit/`) — “kit overview / buy intent”
Suggested options:
- `DIY Voice-Controlled Quadruped Robot Kit — Assembly + Walking Demo | ESP32 AI Lab`
- `Voice-Controlled Quadruped Robot Kit (DIY) — What’s Included + Demo | ESP32 AI Lab`

### Product page (`/product/diy-voice-quadruped-robot-kit/`) — “purchase / SKU page”
Suggested options:
- `DIY Voice-Controlled Quadruped Robot Kit — Price, Shipping, Order | ESP32 AI Lab`
- `Voice Quadruped Robot Kit — Buy, Options, Shipping | ESP32 AI Lab`

Notes:
- Keep the primary keyword near the front; reserve “demo” for one page (prefer kit page).

---

## Meta description recommendations (single, non-duplicated)
Goal: 1 meta description per page, ~150–160 chars, aligned with page intent.

### Kit page (overview)
- “Build a DIY voice-controlled quadruped robot: what’s included, key movement modes, and an assembly + walking demo for STEM learning and robotics practice.”

### Product page (order intent)
- “Order the DIY voice-controlled quadruped robot kit—see what’s included, launch pricing, shipping notes, and the assembly/movement demo before you buy.”

Implementation note: remove the extra meta description output causing `meta_description_count=2`.

---

## H1 / H2 guidance
### H1
- Current H1 is present and clear: `DIY Voice-Controlled Quadruped Robot Kit`
- Keep one H1 only (already true).

### H2 (structure + clarity)
Current H2 set is strong; refine for scanability and reduce repetition:
- Keep commerce H2 (`Order This Kit`, `Shipping & Quote`) but ensure the “learning” sections come first on the kit page.
- Rename the demo H2 to be more descriptive and less repetitive, e.g.:
  - `Assembly + Movement Demo (Video)`
- Consider consolidating image-related sections:
  - `Product Photo` + `Gallery` → `Photos (Current Kit Version)` if the page feels long.
- “Need a different version?” can be made more searchable:
  - `Color / Code Options` or `Need a Different Variant?`

---

## FAQ ideas (add to kit page + optionally product page)
Use these as FAQ blocks (keep answers practical and non-promissory):
1) “What tools do I need for assembly?”
2) “How do I confirm each servo is installed in the correct orientation?”
3) “What’s the safest first movement test before walking forward/backward?”
4) “My robot jitters or drifts—what should I check first?”
5) “How does voice interaction work, and what are the basic limitations?”
6) “What’s included in the box vs. what I must prepare separately?”
7) “Can I use this as a base for custom movement modes or a different controller board?”
8) “What should I do if a leg binds or a screw doesn’t align during assembly?”

---

## Schema (JSON-LD) recommendations
No schema was detected; add JSON-LD where it matches reality:

### Kit page
- `Product` (even if it’s a kit landing page, it still describes a purchasable item)
- `FAQPage` (if you add the FAQ section)
- `VideoObject` (only if a video is embedded for the assembly/movement demo)
- `BreadcrumbList`

### Product page
- `Product` (primary), including price/availability fields only if maintained accurately
- `BreadcrumbList`
- `FAQPage` (optional; keep short to avoid duplicating the kit page)

### Tutorials hub (`/tutorials/`)
- `CollectionPage` or `ItemList` (list of tutorial entries)
- `BreadcrumbList`

---

## Internal linking recommendations (workflow-friendly)
- Add a “Start here: Assembly + movement test guide” link once the tutorial exists:
  - Target: `/tutorials/voice-quadruped-robot-assembly-guide/`
  - Best placements: under **What You Can Explore** and near **Watch the assembly and movement demo**
- From the new tutorial, link back to:
  - Kit page: https://feigen8n.online/kits/diy-voice-quadruped-robot-kit/
  - Product page: https://feigen8n.online/product/diy-voice-quadruped-robot-kit/
- Tutorials hub: add the new tutorial entry with an anchor that matches intent (assembly + movement test).

---

## Publishing risks / checks before going live
- **Meta description duplication**: fix to `count=1` per page to avoid snippet instability.
- **Title duplication between kit and product URLs**: differentiate to avoid internal competition.
- **Schema absence**: adding JSON-LD is low-risk, but only if fields (price/availability/video) stay accurate over time.
- **Tutorial link timing**: don’t link to `/tutorials/voice-quadruped-robot-assembly-guide/` until the page is published (avoid 404s and wasted crawl budget).
- **Demo claims**: keep language aligned with what the page actually shows (avoid implying verified performance beyond the embedded demo/media).
- **Repeated CTA anchors** (“Add to Cart” / “Buy Now” appearing multiple times): fine for UX, but avoid excessive near-duplicate blocks that bloat the page without adding content value.
