# Internal + External Link Plan (STM32 Self-Balancing Car Kit) — 2026-04-30

## Objectives
This plan strengthens discovery and task flow for readers who want a **setup + validation checklist** before attempting balance control and PID tuning. The intent is to connect three existing hubs—**Tutorials**, the **Kit** page, and the **Product** page—without adding sitewide footer links. Every suggested placement keeps wording cautious because kit revisions vary and every “pass” must be confirmed on the user’s own hardware.

---

## Recommended Internal Links (8)

### 1) Tutorials hub → setup tutorial (primary discovery)
- **Source URL:** https://feigen8n.online/tutorials/
- **Target URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Anchor text:** “STM32 self-balancing car setup and PID calibration checklist”
- **Placement rationale:** Keep this link visible inside the STM32 balancing car tutorial listing so visitors browsing tutorials can reach the checklist in one click.
- **Safety notes:** Avoid phrasing that implies a guaranteed outcome (for example, “will balance immediately”). Keep the item described as a checklist that depends on the specific kit revision.

### 2) Tutorials hub → kit page (commercial path without pushing checkout)
- **Source URL:** https://feigen8n.online/tutorials/
- **Target URL:** https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- **Anchor text:** “STM32 Self-Balancing Car Kit”
- **Placement rationale:** Add a secondary link on the same tutorial card (or a short “Kit page” link next to the title) so readers can check what the kit is before starting the checklist.
- **Safety notes:** Do not add “Buy Now” language on the Tutorials hub. Keep the link informational and avoid urgent sales wording.

### 3) Setup tutorial → kit page (context for what the checklist applies to)
- **Source URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Target URL:** https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- **Anchor text:** “STM32 Self-Balancing Car Kit (kit page)”
- **Placement rationale:** Place near the top of the tutorial in a short “About this guide / kit variations” paragraph so readers can compare their hardware to the kit overview before following the steps.
- **Safety notes:** Explicitly state that kit contents, wiring, and firmware can differ by seller and revision. Do not claim the tutorial matches every board/IMU/motor combo.

### 4) Setup tutorial → product page (pricing/stock details without derailing the guide)
- **Source URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Target URL:** https://feigen8n.online/product/stm32-self-balancing-car-kit/
- **Anchor text:** “STM32 Self-Balancing Car Kit (product page)”
- **Placement rationale:** Put in a small “Parts and ordering notes” line near the end of the tutorial so the main setup flow stays technical-first while still providing a direct reference for availability.
- **Safety notes:** Avoid implying that purchasing is required to use the checklist. Keep it as an optional reference link.

### 5) Kit page → setup tutorial (move readers from product interest to safe bring-up)
- **Source URL:** https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- **Target URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Anchor text:** “Setup and PID calibration checklist”
- **Placement rationale:** In the kit page’s “Related setup guides” area, ensure the first tutorial link uses an action-oriented anchor that signals validation steps (IMU checks, motor direction, PID tuning checklist) rather than a vague “read more.”
- **Safety notes:** Keep the surrounding text explicit that steps are only “complete” after the user confirms behavior on their own hardware. Do not suggest any unverified test results.

### 6) Product page → setup tutorial (reduce returns and support load)
- **Source URL:** https://feigen8n.online/product/stm32-self-balancing-car-kit/
- **Target URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Anchor text:** “STM32 self-balancing robot setup checklist”
- **Placement rationale:** Add the link close to “Related setup guides” so buyers can find the safety-first bring-up process immediately after landing on the product page.
- **Safety notes:** Do not promise that following the checklist guarantees stable balancing. Keep expectations realistic and framed as troubleshooting and calibration guidance.

### 7) Kits index → kit page (category navigation that supports search intent)
- **Source URL:** https://feigen8n.online/kits/
- **Target URL:** https://feigen8n.online/kits/stm32-self-balancing-car-kit/
- **Anchor text:** “STM32 Self-Balancing Car Kit”
- **Placement rationale:** Ensure the kits listing card/title links directly to the kit page so users searching for the kit name can move from category browsing to the detailed page quickly.
- **Safety notes:** Keep the card description factual (PID control, IMU, encoder motors) and avoid adding claims that are not confirmed by the kit page content.

### 8) Projects hub → setup tutorial (capture robotics learners earlier)
- **Source URL:** https://feigen8n.online/projects/
- **Target URL:** https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/
- **Anchor text:** “Self-balancing robot setup and PID tuning checklist”
- **Placement rationale:** Add a projects entry (or a short “Robotics control” section) that links to the tutorial so visitors exploring projects can reach a hands-on calibration workflow.
- **Safety notes:** Do not present the project as “verified on all kits.” Keep the language framed as a learning checklist and point users back to the kit page for revision differences.

---

## Authoritative External References (2)
These external links should live in the setup tutorial under a short “Official references” section and should not be framed as reciprocal partnerships.

1) **STM32Cube documentation (STM32CubeIDE)**
- **URL:** https://www.st.com/en/development-tools/stm32cubeide.html
- **Suggested anchor:** “STM32CubeIDE documentation (ST)”
- **Safety note:** State that the IDE UI and steps can change across versions.

2) **ST motor control resources**
- **URL:** https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html
- **Suggested anchor:** “ST motor control ecosystem resources”
- **Safety note:** Keep it positioned as background learning for motor control concepts and tooling, not as required reading.

---

## Implementation Guardrails
- Do not add sitewide footer links or repetitive keyword-stuffed anchors. Use natural anchors that still reflect the page topic.
- Keep every checklist step framed as “verify on your hardware,” and avoid any statements that imply hardware tests were completed during this workflow.
