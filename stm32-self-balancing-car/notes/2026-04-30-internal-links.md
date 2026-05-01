# Internal + External Link Plan — STM32 Self-Balancing Car Setup & PID Calibration Checklist (2026-04-30)

## Goals
This plan strengthens discoverability for the “STM32 self-balancing car setup and PID calibration checklist” tutorial by connecting it to high-intent commerce pages (kit/product) and the Tutorials hub, while keeping claims verifiable and revision-safe. Each internal link below is specific (page-to-page), uses descriptive anchor text, and avoids sitewide placements.

## Recommended internal links (8)

1) **Source URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`  
   **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Anchor text:** “STM32 self-balancing car setup and PID calibration checklist”  
   **Placement rationale:** Place under the existing “Related setup guides” area to match user intent right after they decide to buy or compare the kit, because this section already frames a practical bring-up flow.  
   **Safety notes:** Keep the surrounding copy checklist-focused and revision-agnostic, and avoid promising a guaranteed tuning result on all hardware revisions.

2) **Source URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`  
   **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Anchor text:** “setup and PID calibration checklist”  
   **Placement rationale:** Mirror the kit-page behavior on the product page so shoppers arriving via product listings can immediately access the bring-up steps without backtracking.  
   **Safety notes:** Avoid phrasing that implies the tutorial is a substitute for safe bench testing, and remind readers to confirm IMU and motor direction on their own build.

3) **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Target URL:** `https://feigen8n.online/kits/stm32-self-balancing-car-kit/`  
   **Anchor text:** “STM32 Self-Balancing Car Kit”  
   **Placement rationale:** Add a short “Related kit page” line near the top of the tutorial for users who started from search intent (“PID tuning checklist”) and then want the exact kit context and photos.  
   **Safety notes:** Keep this link informational, and do not insert pricing claims inside the tutorial body unless they are guaranteed to stay accurate.

4) **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Target URL:** `https://feigen8n.online/product/stm32-self-balancing-car-kit/`  
   **Anchor text:** “product page for ordering and shipping details”  
   **Placement rationale:** Place near the end of the tutorial after the checklist, when the reader has validated the workflow and is ready to purchase or confirm what is included.  
   **Safety notes:** Do not include urgency language, and avoid implying that the product page contains firmware downloads unless that is explicitly present.

5) **Source URL:** `https://feigen8n.online/tutorials/`  
   **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Anchor text:** “STM32 self-balancing car setup and PID calibration checklist”  
   **Placement rationale:** Ensure the Tutorials hub entry remains prominent and matches the exact search intent terms (“setup,” “PID,” “checklist”), because the hub page has no H2 sections and benefits from clear scannable anchors.  
   **Safety notes:** Keep the hub description factual and avoid adding claims about supported STM32 variants unless the tutorial states them.

6) **Source URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Target URL:** `https://feigen8n.online/tutorials/`  
   **Anchor text:** “Tutorials”  
   **Placement rationale:** Add a breadcrumb-style link near the top so users can navigate to other guides after finishing PID bring-up, improving session depth without a sitewide footer link.  
   **Safety notes:** Keep it as a simple navigation aid, and do not stack multiple hub links in the same paragraph.

7) **Source URL:** `https://feigen8n.online/tutorials/esp32-sensor-dashboard/`  
   **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Anchor text:** “robot bring-up checklist style (STM32 self-balancing car)”  
   **Placement rationale:** Add a contextual “If you like checklist-based validation” cross-link near a troubleshooting or validation-oriented section to route readers who prefer stepwise testing into a robotics control example.  
   **Safety notes:** Avoid suggesting the ESP32 tutorial requires STM32 hardware, and keep the cross-link optional and clearly labeled as a related learning path.

8) **Source URL:** `https://feigen8n.online/tutorials/esp32-s3-camera-ai-vision-starter/`  
   **Target URL:** `https://feigen8n.online/tutorials/stm32-self-balancing-car-setup/`  
   **Anchor text:** “PID tuning checklist for a two-wheel balancing robot (STM32)”  
   **Placement rationale:** Place as a “Next project” suggestion for readers who finish a camera bring-up and want a control-systems challenge, because both topics attract hands-on builders who follow structured setup steps.  
   **Safety notes:** Do not imply that the balancing car tutorial includes camera integration, and keep the anchor text narrowly scoped to PID and setup.

## Authoritative external references (3)
- **STM32CubeIDE documentation (STMicroelectronics):** `https://www.st.com/en/development-tools/stm32cubeide.html`  
  Use as the primary official reference for STM32 development environment setup, and link from the tutorial section that mentions firmware build or IDE setup.

- **ST motor control resources (STMicroelectronics):** `https://www.st.com/content/st_com/en/ecosystems/stm32-motor-control-ecosystem.html`  
  Use as an authoritative reference when discussing motor control concepts, PWM setup, or motor/driver considerations in a balancing robot context.

- **Tutorials hub (internal-but-authoritative navigation reference):** `https://feigen8n.online/tutorials/`  
  Use as the canonical “more guides” destination instead of adding broad external blog links, because it is stable and already curated for the site.

## Implementation notes
Each placement should be inside an existing relevant section (for example, “Related setup guides,” a short “Related” block in the tutorial, or a “Next project” paragraph), and every link should be surrounded by wording that stays true across kit revisions and does not claim unverified hardware test outcomes.
