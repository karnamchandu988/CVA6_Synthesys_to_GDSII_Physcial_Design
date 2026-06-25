<div align="center">

# 🧠 CVA6 RISC-V Core — Synthesis-to-GDSII Physical Design

### A macro-dominant backend implementation using Design Compiler + IC Compiler II

![Status](https://img.shields.io/badge/Status-Signoff%20Clean-2EC4B6?style=flat-square)
![DRC](https://img.shields.io/badge/DRC%20Violations-0-2EC4B6?style=flat-square)
![Timing](https://img.shields.io/badge/WNS%2FTNS-0%20ns-2EC4B6?style=flat-square)
![Frequency](https://img.shields.io/badge/Frequency-666.66%20MHz-0D1B2A?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-FF9F1C?style=flat-square)

</div>

<br>

<!-- 🖼️ MAIN IMAGE — paste your GitHub-hosted screenshot URL here (see outputs.md for how) -->
<p align="center">
  <img src="https://github.com/user-attachments/assets/346ec057-ecf7-4a59-a2a3-8c246dfca518" alt="CVA6 Post-Route Block" width="85%">
  <br>
  <em>Final routed view of the CVA6 core — see outputs.md for the full screenshot breakdown</em>
</p>

<br>

## 📑 Table of Contents
- [The Story](#-the-story)
- [Project Specifications](#-project-specifications)
- [Design Flow](#-design-flow)
- [The Congestion Problem & The Fix](#-the-congestion-problem--the-fix)
- [Results Summary](#-results-summary)
- [Tools & Methodology](#-tools--methodology)
- [Repository Structure](#-repository-structure)
- [Screenshot Gallery](#-screenshot-gallery)
- [Key Learnings](#-key-learnings)
- [Author](#-author)
- [License](#-license)

<br>

## 🧩 The Story

This project takes the **CVA6 RISC-V core** through a complete **Synthesis-to-GDSII** backend flow — starting from RTL synthesis in **Design Compiler (DC)** with hand-written SDC and constraint scripts, through to a fully routed, sign-off-clean layout in **IC Compiler II (ICC2)**.

The design is **macro-dominant** — 24 SRAM macros (instruction/data caches and register banks) sitting right in the middle of the floorplan. That single fact shaped almost every decision in this project: macro-heavy floorplans are notorious for creating **routing congestion** and **local cell-density spikes** around the macro boundaries, and this design was no exception.

The core engineering story here is how those two problems were diagnosed (density heatmaps, congestion maps) and resolved (partial blockages + cell padding) — and how fixing them also pulled the design's timing back to a clean closure.

> 💡 All screenshots were captured from a cloud-based EDA environment (local file export wasn't available), so this repo uses GitHub's comment-image hosting trick — see [`outputs.md`](outputs.md) for the full gallery and how to wire the images in.

<br>

## 📐 Project Specifications

| Parameter | Value |
|---|---|
| Design | CVA6 RISC-V Core |
| Flow | Synthesis-to-GDSII (DC + ICC2) |
| Design Type | Macro-dominant |
| Macro Count | 24 |
| Leaf Cell Count | 219,738 |
| Hierarchical Cell Count | 335 |
| Combinational Cells | 196,184 |
| Sequential Cells | 23,554 (incl. 325 clock-gating cells) |
| Total Nets | 225,692 |
| Clock Period | 1.5 ns |
| Clock Frequency | **666.66 MHz** |
| WNS — Setup | 0 ns |
| WNS — Hold | 0 ns |
| Critical Paths | 2, slack ≈ -0.0001 ns (negligible) |
| CTS Buffer Levels | 20 |
| Nets with Violations | 0 |
| Max Transition / Max Cap Violations | 0 / 0 |
| Placement Legality | Clean |
| Total Cell Area (cells + macros) | 711,188.23 µm² |
| Total Cell Area (incl. physical-only cells) | 728,419.99 µm² |
| Macro / Black-Box Area | 435,423.12 µm² |
| Total Net Length | 7,530,539.62 µm |
| **Utilization** | `(Total Cell Area ÷ Core Area) × 100` — plug in your Core Area from the floorplan setup to complete this (not visible in the shared reports) |

<br>

## 🛣️ Design Flow

<details>
<summary><b>1️⃣ Synthesis — Design Compiler (DC)</b></summary>
<br>

RTL synthesized in DC using custom-written SDC constraints and scripts (not reference/default scripts) — clock definitions, I/O delays, and design rule constraints set up from scratch to match the target 1.5 ns period.

</details>

<details>
<summary><b>2️⃣ Floorplanning — IC Compiler II</b></summary>
<br>

Macro placement for all 24 SRAM macros, followed by power/ground mesh and routing grid setup.

<img src="PASTE_URL_HERE" alt="Floorplan" width="80%">

</details>

<details>
<summary><b>3️⃣ Placement</b></summary>
<br>

Standard cell placement around the fixed macros — this is where the density problem first became visible.

<img src="PASTE_URL_HERE" alt="Placement" width="80%">

</details>

<details>
<summary><b>4️⃣ Congestion & Density Fix</b></summary>
<br>

Partial blockages added around macro boundaries + cell padding applied to relieve local density — see the dedicated section below.

<img src="PASTE_URL_HERE" alt="Congestion Fix" width="80%">

</details>

<details>
<summary><b>5️⃣ Clock Tree Synthesis (CTS)</b></summary>
<br>

20-level clock tree built to keep skew and insertion delay under control across the macro-heavy block.

<img src="PASTE_URL_HERE" alt="CTS" width="80%">

</details>

<details>
<summary><b>6️⃣ Routing & Signoff</b></summary>
<br>

Full routing completed with 0 DRC violations and clean placement legality.

<img src="PASTE_URL_HERE" alt="Routing" width="80%">

</details>

<br>

## ⚙️ The Congestion Problem & The Fix

| | |
|---|---|
| **The problem** | A 24-macro floorplan left dense, irregular standard-cell channels around the macros — the density heatmap showed clear hotspots, and the congestion map showed demand outstripping routing supply in those same zones. |
| **The fix** | Added **partial blockages** around macro boundaries to steer the placer away from the tightest channels, then applied **cell padding** to space out standard cells and ease local density. |
| **The side benefit** | Resolving congestion shortened the indirect routes the placer had been forced into — which in turn pulled timing back to a clean **0 ns WNS/TNS**. |

<br>

## ✅ Results Summary

- 🎯 **Timing:** Clean across setup and hold (WNS = TNS = 0 ns); 2 critical paths at negligible slack (~0.0001 ns)
- 🧱 **Congestion:** Fully resolved via partial blockages + cell padding
- 🕐 **CTS:** Balanced clock tree, 20 buffer levels
- 🛣️ **Routing:** 100% complete, **0 DRC violations** across 225,692 nets
- 📐 **Legality:** Placement legality check — clean

<br>

## 🔧 Tools & Methodology

- **Synthesis:** Synopsys **Design Compiler (DC)**
- **Backend (Floorplan → Place → CTS → Route → Signoff):** Synopsys **IC Compiler II (ICC2)**
- **Constraints:** SDC and supporting TCL scripts written from scratch for this design — not pulled from a reference/template flow
- **Flow:** Synthesis-to-GDSII

<br>

## 📂 Repository Structure

```
cva6-physical-design-implementation/
├── outputs.md          # full screenshot gallery with titles & captions
├── README.md
└── LICENSE
```

> 📌 Screenshots are hosted via GitHub's comment-image trick (see `outputs.md`) rather than committed as binary files — keeps the repo lean.

<br>

## 🖼️ Screenshot Gallery

The full, titled set of screenshots — floorplan, density/congestion maps, the blockage fix, CTS, post-route detail, and final sign-off reports — lives in **[`outputs.md`](outputs.md)**, along with instructions for hosting the images on GitHub.

<br>

## 🚀 Key Learnings

- Diagnosing congestion and density issues using heatmaps **before** they show up as routing failures
- Using **partial blockages** and **cell padding** as practical, targeted fixes in a macro-dominant floorplan
- Writing **custom SDC and constraint scripts** instead of relying on default/reference flows
- Building a balanced **20-level clock tree** for a macro-heavy design
- Closing a **219,738-instance** design with **0 DRC violations** and clean timing

<br>

## 👤 Author

**[Your Name]**
🔗 [LinkedIn](#) · [GitHub](#) · [Email](#)

<br>

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---
<div align="center">
⭐ If you found this project useful or interesting, consider giving it a star!
</div>
