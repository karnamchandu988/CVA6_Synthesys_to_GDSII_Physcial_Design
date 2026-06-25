# 📸 Project Outputs — Screenshot Gallery

This file documents every stage of the **CVA6 RISC-V Core — Synthesis-to-GDSII** flow, captured directly from the cloud EDA environment (Design Compiler + IC Compiler II).

---


## Screenshot 1 — Initial Floorplan: Macro Placement Overview

24 SRAM macros placed across the floorplan — `gen_256x45` and `gen_256x128` instruction/data SRAM banks on the left, `as_4x128 sram_bank[0–3]` banks on the right. This macro layout is what drove every congestion and density decision later in the flow.

![Screenshot 1 - Initial Floorplan](PASTE_URL_HERE)

---

## Screenshot 2 — Full-Chip Placement View

Zoomed-out view after standard cell placement, showing the relationship between the dense central cell region and the macro columns on either side.

![Screenshot 2 - Full-Chip Placement](PASTE_URL_HERE)

---

## Screenshot 3 — Zoomed Floorplan View: PG Mesh / Routing Grid

A close-up of the power/ground mesh and routing grid set up during floorplanning in IC Compiler II (`cva6_S_floorplan.design`).

![Screenshot 3 - PG Mesh Zoom](PASTE_URL_HERE)

---

## Screenshot 4 — Cell Density Heatmap (Issue Identified)

Density map of the design — green/yellow/orange regions near the macros flagged the high cell-density zones that needed to be addressed before routing.

![Screenshot 4 - Cell Density Heatmap](PASTE_URL_HERE)

---

## Screenshot 5 — Channel Congestion Map (After Fix)

Congestion map (total demand minus total supply) after applying the fix — almost the entire design sits in the "0" congestion bin, confirming the congestion issue was resolved.

![Screenshot 5 - Congestion Map Clean](PASTE_URL_HERE)

---

## Screenshot 6 — Partial Blockages Around Macros (The Fix)

Colored blockage regions added around the macro boundaries to steer standard cell placement away from congestion-prone zones — this, combined with cell padding, was the core fix for both the congestion and density issues.

![Screenshot 6 - Partial Blockages](PASTE_URL_HERE)

---

## Screenshot 7 — Clock Tree Synthesis: Buffer Levels

Clock tree structure showing the buffer/inverter stages from the clock root down to the leaf sinks — built out to **20 levels** to manage skew and insertion delay across the macro-heavy block.

![Screenshot 7 - CTS Buffer Levels](PASTE_URL_HERE)

---

## Screenshot 8 — Post-Route Layout (Detailed View)

Fully routed view of `cva6_S_postroute.design`, showing the complete metal stack (M1–M9, VIA1–VIA8) and standard cell instances after routing.

![Screenshot 8 - Post-Route Detail](PASTE_URL_HERE)

---

## Screenshot 9 — Sign-off Report: Cell Count Summary

Final cell count report — **219,738 leaf cells**, **24 sequential macros**, 23,554 sequential cells (325 clock-gating cells), 196,184 combinational cells, 0 isolation/level-shifter violations.

![Screenshot 9 - Cell Count Report](PASTE_URL_HERE)

---

## Screenshot 10 — Sign-off Report: Area & Design Rule Summary

Final area breakdown (cell area, macro area, net length) and design rule summary — **225,692 total nets, 0 nets with violations, 0 max-transition and 0 max-cap violations.**

![Screenshot 10 - Area & DRC Report](PASTE_URL_HERE)

---

*(Add Screenshots 11–20 here in the same format as you upload the rest.)*
