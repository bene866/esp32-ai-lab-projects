# Internal Link + Official Reference Plan (STM32 Self‑Balancing Car Kit)

This page proposes a clear, low-risk linking structure between the STM32 self‑balancing car kit/product pages and the setup + PID tuning tutorial(s). The intent is to help readers find the right checklist quickly, set expectations early, and reduce avoidable support issues caused by board/IMU/motor-driver variations.

## Linking principles (public-safe)
- **Be verification-first:** Use wording like “check,” “confirm,” “validate on your kit,” and “your board revision may differ.”
- **Avoid hard assumptions:** Do not imply a fixed IMU model, fixed pinout, fixed motor driver, encoder presence, or guaranteed balance performance.
- **Keep the tutorial technical-first:** Put commerce links later in the tutorial flow, after safety checks and “what to verify” sections.
- **Prefer context-rich anchors:** Anchors like “setup checklist” and “PID tuning order” signal practical content and reduce wrong clicks.
- **Don’t over-link:** One strong link per section usually beats repeated links in the same block.

---

## Recommended internal links (8)

### 1) Tutorials hub → STM32 setup tutorial
- **Source URL:** `https://feigen8n.online/tutorials/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Suggested anchor text:** `STM32 self‑balancing car setup checklist (wiring checks + PID tuning order)`
- **Placement rationale:** Put in the primary tutorials list near the top so “STM32 self balancing robot setup” visitors don’t have to scan or guess.
- **Safety copy note:** Keep “checklist” and “checks” to reinforce that readers should validate against their specific kit revision.

### 2) Kit page → STM32 setup tutorial (primary onboarding path)
- **Source URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Suggested anchor text:** `Read the setup checklist`
- **Placement rationale:** Add to a “Related setup guides” section and keep it above any optional extras.
- **Suggested one-line description (verification tone):** “Use this checklist to confirm wiring, sensor orientation/sign, and a safe tuning sequence—your board/IMU revision may differ, so validate each step on your hardware.”

### 3) Product page → STM32 setup tutorial (pre‑purchase expectation-setting)
- **Source URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Suggested anchor text:** `Setup + PID tuning checklist`
- **Placement rationale:** Place in “Related setup guides” so buyers understand the workflow before checkout and can self-serve common issues.
- **Safety copy note:** Avoid wording like “guarantees balancing” or “works out of the box.” Emphasize “step-by-step verification.”

### 4) STM32 setup tutorial → Kit page (photos + general context)
- **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Target URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Suggested anchor text:** `STM32 Self‑Balancing Car Kit`
- **Placement rationale:** Put one link in the tutorial intro (after “who this is for”) so readers can compare their kit to the typical product photos and page description before wiring.
- **Safety copy note:** Use neutral phrasing like “See the kit page for photos and the typical configuration.” Do not imply the tutorial requires this exact kit.

### 5) STM32 setup tutorial → Product page (secondary purchase path)
- **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Target URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Suggested anchor text:** `STM32 self‑balancing car kit`
- **Placement rationale:** Place near the end of the tutorial, after the reader has completed safety checks and has a “next steps” section.
- **Safety copy note:** Keep it optional and non-urgent; avoid pricing, availability, and performance claims.

### 6) Kit page → Tutorials hub (broader exploration)
- **Source URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/`
- **Suggested anchor text:** `More build guides`
- **Placement rationale:** Add one link under “What you can learn next” or “More guides” for visitors comparing platforms or looking for adjacent robotics tutorials.
- **Safety copy note:** Keep the link inside a relevant section (not repeated in multiple blocks) to avoid feeling like boilerplate.

### 7) Product page → Tutorials hub (post‑purchase learning fallback)
- **Source URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/`
- **Suggested anchor text:** `Tutorials`
- **Placement rationale:** Near “Related setup guides,” this provides a way out if a reader needs general embedded setup background (toolchain, flashing, debugging).
- **Safety copy note:** Frame as optional learning resources, not a checkout requirement.

### 8) Projects page → Kit page (category discovery)
- **Source URL:** `https://feigen8n.online/projects/`
- **Target URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Suggested anchor text:** `STM32 Self‑Balancing Car Kit`
- **Placement rationale:** Add a single contextual link in the robotics/self-balancing area of the projects listing so browsing users can discover the kit page naturally.
- **Safety copy note:** Avoid duplicating the same link multiple times in one projects section.

---

## Where to place “revision varies” reminders (recommended)
To reduce wrong-expectation risk without sounding defensive, use short reminders in two places:
- **Early (tutorial + kit/product pages):** “Board/IMU/motor driver revisions vary—confirm labels, pinout, and orientation on your hardware before powering motors.”
- **Before closed-loop tuning steps:** “If the robot falls harder when enabled, stop and re-check motor direction and IMU axis/sign assumptions.”

These reminders should be short, actionable, and paired with a “what to check next” link (usually the setup checklist).

---

## Authoritative official references (2–3)

1) **STM32CubeIDE (official ST page)**
- **URL:** `https://www.st.com/en/development-tools/stm32cubeide.html`
- **Best placement:** In the tutorial section that discusses toolchain setup, importing/building projects, flashing, or debugging.
- **Safety note:** Keep it as an official reference for installation and documentation. Avoid “disable security checks” style instructions.

2) **ST motor control ecosystem (official ST overview)**
- **URL:** `https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html`
- **Best placement:** As optional background reading in sections explaining motor direction, control sign conventions, and safe test workflow.
- **Safety note:** Present as supplemental learning, not a required dependency for the kit.

3) **Use only if it clarifies terminology (avoid duplicates)**
- **URL:** `https://www.st.com/en/development-tools/stm32cubeide.html`
- **Best placement:** If “STM32Cube” terminology appears and readers may confuse CubeIDE vs CubeMX, include a single clarification link rather than repeating multiple external links.
- **Safety note:** Prefer one authoritative link per concept to keep pages clean and reduce distraction.
