# 📸 Project Outputs — Screenshot Gallery

This file documents every stage of the **CVA6 RISC-V Core — Synthesis-to-GDSII** flow, captured directly from the cloud EDA environment (Design Compiler + IC Compiler II).

---


## Screenshot 1 — Initial Floorplan: Macro Placement Overview

24 SRAM macros placed across the floorplan — `gen_256x45` and `gen_256x128` instruction/data SRAM banks on the left, `as_4x128 sram_bank[0–3]` banks on the right. This macro layout is what drove every congestion and density decision later in the flow.

![Screenshot 1 - Initial Floorplan](https://github.com/user-attachments/assets/d93a7bc5-ec00-4080-a05a-99e8d5d2be01)

---

## Screenshot 2 — Full-Chip Placement View

Zoomed-out view after standard cell placement, showing the relationship between the dense central cell region and the macro columns on either side.

![Screenshot 2 - Full-Chip Placement](https://github.com/user-attachments/assets/021cf4bc-7563-42bd-9317-079bc519b48c)

---

## Screenshot 3 — Zoomed Floorplan View: PG Mesh / Routing Grid

A close-up of the power/ground mesh and routing grid set up during floorplanning in IC Compiler II (`cva6_S_floorplan.design`).

![Screenshot 3 - PG Mesh Zoom](https://github.com/user-attachments/assets/ae9d0871-2bd2-49ac-9802-02e41711acde)

---

## Screenshot 4 — Cell Density Heatmap (Issue Identified)

Density map of the design — green/yellow/orange regions near the macros flagged the high cell-density zones that needed to be addressed before routing.

![Screenshot 4 - Cell Density Heatmap](https://github.com/user-attachments/assets/8333ec99-b4c7-4933-9c0a-9d5a8268ee61)

---

## Screenshot 5 — Channel Congestion Map (After Fix)

Congestion map (total demand minus total supply) after applying the fix — almost the entire design sits in the "0" congestion bin, confirming the congestion issue was resolved.

![Screenshot 5 - Congestion Map Clean](https://github.com/user-attachments/assets/6357d5b6-f9e4-4033-b0cc-bab34a3918c7)

---


## Screenshot 6 — Clock Tree Synthesis: Buffer Levels

Clock tree structure showing the buffer/inverter stages from the clock root down to the leaf sinks — built out to **20 levels** to manage skew and insertion delay across the macro-heavy block.

![Screenshot 6 - CTS Buffer Levels](https://github.com/user-attachments/assets/8a17eb6c-2418-414a-a51f-60dc34c58023)

---

## Screenshot 7 — Post-Route Layout (Detailed View)

Fully routed view of `cva6_S_postroute.design`, showing the complete metal stack (M1–M9, VIA1–VIA8) and standard cell instances after routing.

![Screenshot 7 - Post-Route Detail](https://github.com/user-attachments/assets/5a67fe37-7f43-40d8-9b08-f23d2f1f48bc)

---

## Screenshot 8 — Sign-off Report: Cell Count Summary

Final cell count report — **219,738 leaf cells**, **24 sequential macros**, 23,554 sequential cells (325 clock-gating cells), 196,184 combinational cells, 0 isolation/level-shifter violations.

![Screenshot 8 - Cell Count Report](https://github.com/user-attachments/assets/c1c4e0f5-0a6d-436a-ad45-81293332d397)

---

## Screenshot 9 — Sign-off Report: Area Summary

Final area utilization report showing the breakdown of standard-cell area, macro area, physical-only cell area, and total net length after successful routing and sign-off.

![Screenshot 9 - Area Report](https://github.com/user-attachments/assets/de434896-48f4-4ba3-8dc1-2232ec65e8dc)

---
## Screenshot 10 — Global Timing Report

Final post-route global timing summary generated after sign-off optimization. The design achieves **no hold violations**, with only **5 negligible setup violations** (2 reg-to-reg and 3 input-to-register paths), each reporting a worst negative slack of approximately **-0.00 ns**, indicating timing closure is effectively achieved within reporting precision.

![Screenshot 10 - Global Timing Report](https://github.com/user-attachments/assets/906b6b56-aa2b-443a-91e8-92386cdae3c6)

---
## Screenshot 11 — Design Rule Violation (DRV) Summary

Final design rule verification report after sign-off optimization. The design reports **zero design rule violations**, including **0 max transition**, **0 max capacitance**, **0 min capacitance**, and **0 minimum pulse width** violations, confirming compliance with all electrical design constraints.

![Screenshot 11 - Design Rule Violation Summary](https://github.com/user-attachments/assets/e95261ea-8569-4b30-a1f0-166c2bd33989)

---
## Screenshot 12 — DRC Verification Report

Final Design Rule Check (DRC) verification confirming a **clean routed database**. The report shows **0 DRC violations**, **0 antenna violations**, and no extraction or connectivity issues across **225,289 routed nets**, indicating the layout satisfies all physical design rule requirements.

![Screenshot 12 - DRC Verification Report](https://github.com/user-attachments/assets/1c8a8de7-d878-4e29-9d4f-2efaa43d1229)

---
## Screenshot 13 — LVS / Connectivity Verification Report

Final layout connectivity verification confirming a **clean LVS-style verification**. The report indicates **0 short violations**, **0 open nets**, and **0 floating route violations** across **225,692 input nets**, demonstrating correct routing connectivity throughout the design.

![Screenshot 13 - LVS Verification Report](https://github.com/user-attachments/assets/99d9513a-84f1-43bb-836f-f64bf90888c3)

---
## Screenshot 14 — Placement Legality Report

Final placement legality check confirming a **fully legal design**. The report shows **0 violations** for overlap, spacing rules, cell-on-site placement, legal orientation, and power-grid (PG) DRC checks, verifying that all standard cells satisfy placement legality requirements before sign-off.

![Screenshot 14 - Placement Legality Report](https://github.com/user-attachments/assets/9ff98737-539c-43e2-b5be-7d40c4984e8f)

---
## Screenshot 15 — Final GDSII Layout

Final **GDSII database** generated after successful completion of the physical design flow. The layout represents the tape-out-ready implementation of the **CVA6 RISC-V core**, incorporating all floorplanning, placement, clock tree synthesis, routing, and sign-off optimizations into the final manufacturable design database.

![Screenshot 15 - Final GDSII Layout](https://github.com/user-attachments/assets/f6fc64ac-87d3-4f69-a3a6-54a625eacfa3)

---
