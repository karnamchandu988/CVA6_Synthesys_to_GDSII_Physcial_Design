# 📸 Project Outputs — Screenshot Gallery

This file documents every stage of the **CVA6 RISC-V Core — Synthesis-to-GDSII** flow, captured directly from the cloud EDA environment (Design Compiler + IC Compiler II).

---


## Screenshot 1 — Initial Floorplan: Macro Placement Overview

24 SRAM macros placed across the floorplan — `gen_256x45` and `gen_256x128` instruction/data SRAM banks on the left, `as_4x128 sram_bank[0–3]` banks on the right. This macro layout is what drove every congestion and density decision later in the flow.

![Screenshot 1 - Initial Floorplan](https://github.com/user-attachments/assets/d93a7bc5-ec00-4080-a05a-99e8d5d2be01)

---

## Screenshot 2 — Full-Chip Placement View

Zoomed-out view after standard cell placement, showing the relationship between the dense central cell region and the macro columns on either side.

![Screenshot 2 - Full-Chip Placement](https://github.com/user-attachments/assets/dd14f86f-831c-41a5-afb5-d9b8cef04474)

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

## Screenshot 9 — Sign-off Report: Area & Design Rule Summary

Final area breakdown (cell area, macro area, net length) and design rule summary — **225,692 total nets, 0 nets with violations, 0 max-transition and 0 max-cap violations.**

![Screenshot 9 - Area & DRC Report](https://github.com/user-attachments/assets/219a6b57-4c65-4ce8-ac1c-685a80fbed27)

---

*(Add Screenshots 11–20 here in the same format as you upload the rest.)*
