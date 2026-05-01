# Internal + External Link Plan (STM32 Self-Balancing Car Kit)

## Goals
- Help “setup + PID tuning” visitors land on the right checklist page fast.
- Provide a clean path from informational pages (tutorials) to commercial pages (kit/product) without over-selling.
- Reduce wrong-expectation risk by reinforcing that wiring, firmware, and revisions vary by seller and batch.

---

## Recommended internal links (8)

### 1) Tutorials hub → STM32 setup tutorial
- **Source URL:** `https://feigen8n.online/tutorials/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Anchor text:** `STM32 self-balancing car setup and PID calibration checklist`
- **Placement rationale:** Keep this link in the primary tutorial list near the top so “STM32 self balancing robot setup” visitors do not need to scan the full page.
- **Safety notes:** Do not promise a specific board/IMU model. Keep the word “checklist” to signal verification-based steps.

### 2) Kit page → STM32 setup tutorial (primary path)
- **Source URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Anchor text:** `Read setup guide`
- **Placement rationale:** Place this link in the “Related setup guides” section and add one short sentence that clarifies the guide covers IMU checks, motor direction verification, and PID tuning order.
- **Safety notes:** Avoid language that implies the guide matches every “revision.” Keep a reminder that steps are “passed” only after hardware confirmation.

### 3) Product page → STM32 setup tutorial (pre-purchase confidence)
- **Source URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Anchor text:** `STM32 self-balancing car setup and PID calibration checklist`
- **Placement rationale:** In “Related setup guides,” this link reduces support load by setting expectations before checkout and provides a troubleshooting-first route.
- **Safety notes:** Do not claim the tutorial guarantees balance performance. Keep wording focused on checks and tuning workflow.

### 4) STM32 setup tutorial → Kit page (parts/context reference)
- **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Target URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Anchor text:** `STM32 Self-Balancing Car Kit`
- **Placement rationale:** Add this in the tutorial intro (after the “who this is for” paragraph) so readers can confirm what the kit generally includes and see photos before wiring.
- **Safety notes:** Use neutral phrasing like “kit page for photos and included items.” Do not imply the tutorial requires this exact kit.

### 5) STM32 setup tutorial → Product page (purchase path, kept secondary)
- **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`
- **Target URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Anchor text:** `STM32 self balancing car kit`
- **Placement rationale:** Place this link near the end of the tutorial (after the checklist and “safe next actions”) so the content remains technical-first while still offering a clear next step.
- **Safety notes:** Avoid urgency wording. Do not add pricing claims in the tutorial body.

### 6) Kit page → Tutorials hub (exploration without sitewide links)
- **Source URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/`
- **Anchor text:** `More build guides`
- **Placement rationale:** Add one link under “Related setup guides” or near “What You Can Explore” for visitors who are comparing projects (ESP32, STM32, robotics) before deciding.
- **Safety notes:** Keep this contextual to the page section. Do not place it in global navigation or footer copy.

### 7) Product page → Tutorials hub (post-purchase onboarding)
- **Source URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`
- **Target URL:** `https://feigen8n.online/tutorials/`
- **Anchor text:** `Tutorials`
- **Placement rationale:** Near the “Related setup guides” block, this link provides a fallback if the user needs broader embedded setup context or wants other examples.
- **Safety notes:** Do not present as a required step for checkout. Keep it framed as optional learning resources.

### 8) Projects page → Kit page (category discovery)
- **Source URL:** `https://feigen8n.online/projects/`
- **Target URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`
- **Anchor text:** `STM32 Self-Balancing Car Kit`
- **Placement rationale:** Add a single contextual link in the robotics-related area of the projects listing so “robotics project” browsers can discover the kit page directly.
- **Safety notes:** Avoid multiple repeated links on the same page section. Do not turn it into a sitewide template link.

---

## Authoritative external references (2–3)
1) **STM32Cube documentation (STM32CubeIDE)**
   - **URL:** `https://www.st.com/en/development-tools/stm32cubeide.html`
   - **Use in content:** Link from the tutorial section that covers firmware flashing/debug workflow, project import, or build settings.
   - **Safety notes:** Describe it as the official IDE/documentation source. Do not instruct users to disable safety checks or bypass driver warnings.

2) **ST motor control ecosystem resources**
   - **URL:** `https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html`
   - **Use in content:** Link from the tutorial’s motor direction / control concepts section as optional background reading.
   - **Safety notes:** Keep it as reference material, not a required dependency for the kit.

3) **Optional: Link only where it clarifies terminology**
   - **URL:** `https://www.st.com/en/development-tools/stm32cubeide.html`
   - **Use in content:** If the tutorial uses terms like “STM32Cube,” keep a single reference link to avoid duplicate external links.
   - **Safety notes:** Avoid adding multiple near-identical external links on one page.

---
