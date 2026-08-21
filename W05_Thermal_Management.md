# W05 — Robot Electronics Thermal Management Analysis

**Programme:** InGen Dynamics Mechanical Engineer Internship  
**Intern:** Xiaolei Jia  
**Primary platform anchor:** Fari — compact companion robot electronics enclosure  
**Secondary carry-over check:** Sentinel Prime AI sensor package  
**Analysis level:** Preliminary lumped thermal model / pre-PDR screening  
**Units:** SI unless stated otherwise

---

## Executive Finding

**Passive cooling is feasible for the Week 5 Fari screening case, but enclosure area is more important than choosing an ultra-high-conductivity wall material once a reasonable conductive path exists.** Using a representative embedded-AI heat budget of **14.87 W** at the worst programme ambient of **30 °C**, the baseline compact ABS enclosure with only **0.040 m²** effective natural-convection area predicts a junction temperature of **88.5 °C**, which fails the **85 °C** target by **3.5 °C**. A simple aluminium heat spreader that doubles the effective wall-contact area reduces the prediction to **83.6 °C**, passing the junction target without a fan.

The selected passive concept is therefore an **aluminium heat spreader bonded from the compute module/PCB into the enclosure wall, using a medium-conductivity TIM and at least 0.045 m² effective exposed area**. The model predicts **80.1 °C**, leaving about **4.9 °C** junction-temperature margin. An external fin array gives the largest thermal reduction, but it is treated as a secondary option because fins add external geometry to a human-proximate companion robot.

A secondary Week 4 closure check also reproduces the earlier Sentinel Prime AI screening target: for **11.043 W**, **50 °C surface temperature**, and **35 °C ambient**, Churchill–Chu gives an approximate natural-convection area requirement of **0.124 m²** and an equivalent resistance of **1.36 K/W**, matching the Week 4 **≤1.36 K/W** target.

---

## 1. Thermal Problem Context and Scaling

Week 5 asks for a lumped thermal resistance model connecting the earlier RVACS heat-transfer work to compact robot electronics. The physical mechanisms are the same — conduction inside solids and convection from a solid boundary to air — but the dominant scale is different.

| Feature | RVACS dissertation context | Fari Week 5 context |
|---|---|---|
| Characteristic length | Order of 1 m | Order of 0.05–0.10 m |
| Heat source | Reactor-scale thermal load | Embedded electronics, order of 10 W |
| External flow | Forced / buoyancy-affected flow, turbulent modelling relevant | Still indoor air, natural convection |
| Expected Rayleigh regime | Much larger Ra | Order of 10^6 in this model |
| Appropriate method | CFD / turbulence model | Lumped network + laminar Churchill–Chu |

The Week 5 model deliberately does **not** use a turbulence model. Across the sensitivity range, the calculated Rayleigh number is approximately **1.7×10^6 to 4.2×10^6**, well below the order-of-10^9 transition level used for a vertical plate screening analysis. The laminar natural-convection branch is therefore appropriate.

---

## 2. Design Basis and Thermal Network

### 2.1 Heat-load basis

No proprietary Fari electronics bill of materials is available, so the power budget is explicitly a representative modelling input rather than a claimed product specification.

| Heat source | Value | Status / basis |
|---|---:|---|
| Representative embedded AI compute module | 8.87 W | NVIDIA Jetson Orin Nano 4GB, 10 W operating-mode thermal design-guide analogue |
| SoC portion used for junction path | 6.90 W | NVIDIA thermal design guide |
| Additional sensors | 4.00 W | Engineering assumption within programme 2–5 W range |
| Communications module | 2.00 W | Engineering assumption within programme 1–3 W range |
| **Total enclosure heat** | **14.87 W** | Sum |
| Worst-case ambient | **30 °C** | Upper end of Week 5 indoor range |
| Junction-temperature target | **≤ 85 °C** | Week 5 programme target |

The NVIDIA thermal guide reports **R_junction-to-case = 0.218 K/W** for the Orin SoC in the selected analogue. The exact Fari compute device is unknown; this value is therefore used only to build a reproducible pre-PDR thermal path.

### 2.2 Thermal resistance network

The programme primer defines four serial elements:

```text
SoC junction
   |
   |  R_junction-to-case
   v
Package / case
   |
   |  R_case-to-PCB
   v
PCB / mount
   |
   |  R_PCB-to-enclosure
   v
Enclosure wall  <---- distributed heat from sensors, comms and non-SoC module losses
   |
   |  R_enclosure-to-ambient = 1/(h A)
   v
Ambient air
```

This submission keeps the same four physical resistances but uses a **distributed-load refinement**. The SoC heat, **6.90 W**, passes through the junction/package/internal conduction path; the full enclosure heat, **14.87 W**, must leave the enclosure by natural convection. This avoids incorrectly forcing every sensor watt through the SoC package while remaining a lumped model rather than CFD.

The governing temperatures are therefore:

\[
T_{wall} = T_{amb} + \frac{Q_{total}}{hA}
\tag{1}
\]

\[
T_{junction} = T_{wall} + Q_{SoC}
\left(R_{jc}+R_{case-PCB}+R_{mount}+R_{wall,cond}+R_{TIM}\right)
\tag{2}
\]

with

\[
R_{wall,cond}=\frac{t_{wall}}{k_{wall}A_{contact}}
\tag{3}
\]

and the Churchill–Chu correlation for a vertical plate:

\[
Nu_L =
\left[
0.825+
\frac{0.387Ra_L^{1/6}}
{\left(1+(0.492/Pr)^{9/16}\right)^{8/27}}
\right]^2
\tag{4}
\]

\[
h=\frac{Nu_L k_{air}}{L}
\tag{5}
\]

### 2.3 Screening assumptions

| Parameter | Value |
|---|---:|
| Characteristic vertical length, L | 0.10 m |
| Wall thickness | 2.0 mm |
| Baseline thermal contact area | 0.010 m² |
| R_case-to-PCB | 0.15 K/W, assumed |
| Mount/contact resistance | 0.30 K/W, assumed |
| ABS conductivity | 0.18 W/mK, representative |
| 6061 aluminium conductivity | 167 W/mK, representative |
| 304 stainless conductivity | 16.2 W/mK, representative |
| Air k | 0.0273 W/mK |
| Air kinematic viscosity | 1.70×10^-5 m²/s |
| Air thermal diffusivity | 2.42×10^-5 m²/s |
| Radiation | Neglected — conservative for temperature |
| Fan / forced airflow | None |

The enclosure geometry, contact pressure, thermal pad stack, PCB copper fraction and actual Fari electronics are unavailable. Those unknowns are treated as explicit model limitations rather than hidden precision.

---

## 3. Sensitivity Analysis

**The model is most sensitive to exposed natural-convection area.** At 0.040 m², aluminium and stainless steel both pass the 85 °C junction target, while the ABS case is slightly too hot. Once the wall material is moderately conductive, the aluminium-versus-stainless difference is very small because external natural convection becomes the dominant resistance.

| Effective area (m²) | ABS Tj (°C) | Al 6061 Tj (°C) | SS 304 Tj (°C) |
|---:|---:|---:|---:|
| 0.030 | 100.3 | 92.7 | 92.8 |
| 0.040 | 88.5 | 80.8 | 80.9 |
| 0.050 | 81.0 | 73.4 | 73.4 |
| 0.060 | 75.8 | 68.2 | 68.2 |
| 0.080 | 69.0 | 61.3 | 61.4 |
| 0.100 | 64.7 | 57.0 | 57.1 |
| 0.120 | 61.7 | 54.0 | 54.1 |

Minimum area required to reach **Tj ≤ 85 °C** under the stated assumptions:

- **ABS:** 0.0442 m²
- **Al 6061:** 0.0359 m²
- **SS 304:** 0.0360 m²

![Junction temperature sensitivity](W05_Tj_vs_Enclosure_Area.png)

**Physical interpretation.** The conductivity change from ABS to metal matters because the wall/contact path is initially significant. The change from stainless steel to aluminium is much smaller because both make wall conduction small compared with the convection resistance. Therefore, adding usable surface area or fins can be more effective than selecting an extremely high-k wall once a metallic heat path is already present.

At the 0.040 m² baseline, the converged wall temperature is **76.2 °C**, with **h ≈ 8.04 W/m²K** and **Ra ≈ 3.38e+06**. The junction target alone is therefore not enough to guarantee a comfortable external touch temperature for a human-proximate platform. A separate allowable external-surface-temperature requirement should be added when real Fari enclosure geometry and user-contact zones are known.

---

## 4. Passive Cooling Concept Evaluation

### 4.1 Option A — aluminium heat spreader

The heat spreader is modelled as doubling effective contact area from 0.010 to **0.020 m²** and reducing the mount/contact term from 0.30 to **0.15 K/W**. At the same 0.040 m² external area, predicted junction temperature falls from **88.5 °C** to **83.6 °C**.

**Result:** passes the 85 °C target without external geometry changes.

### 4.2 Option B — external aluminium fin array

A screening fin array uses eight fins, each approximately 100 mm wide, 20 mm long and 1 mm thick. With the baseline natural-convection coefficient, the rectangular-fin approximation gives:

\[
m=\sqrt{\frac{2h}{k_{fin}t}}
\tag{6}
\]

\[
\eta_{fin}=\frac{\tanh(mL)}{mL}
\tag{7}
\]

The predicted fin efficiency is **0.987**, so the fins are thermally effective. The effective convection area rises from 0.040 m² to approximately **0.0716 m²**, and the model predicts **71.4 °C** junction temperature.

**Result:** largest thermal improvement, but it adds exposed geometry and should be used only if packaging, cleaning, snagging and human-contact constraints allow it.

### 4.3 Option C — TIM conductivity

For a 0.5 mm interface over 0.002 m²:

| TIM conductivity | TIM resistance | Predicted Tj at baseline |
|---:|---:|---:|
| 0.5 W/mK | 0.500 K/W | 92.0 °C |
| 3 W/mK | 0.083 K/W | 89.1 °C |
| 100 W/mK | 0.0025 K/W | 88.5 °C |

**Result:** higher-k TIM helps, but TIM alone does not fix an enclosure whose dominant bottleneck is external convection area.

![Passive cooling comparison](W05_Passive_Cooling_Comparison.png)

### 4.4 Selected concept

**Selected passive design:** aluminium heat spreader + medium-k TIM + effective natural-convection area **≥0.045 m²**.

For the screening geometry, the model predicts:

- **Tjunction ≈ 80.1 °C**
- Junction margin to target: **4.9 °C**
- No fan required for the stated Week 5 junction-temperature requirement.

The 0.045 m² area should be treated as a **minimum screening target**, not a release dimension. A design review should retain margin because contact resistance, internal recirculation and component clustering are not represented in the lumped model.

---

## 5. Sentinel Prime AI Carry-Over Check from Week 4

Week 4 established an 11.043 W sensor heat load and a 50 °C surface target at 35 °C ambient. Applying Churchill–Chu directly at that surface condition gives:

- **h ≈ 5.93 W/m²K**
- **Ra ≈ 1.13e+06**
- Required area **A ≈ 0.124 m²**
- Equivalent convection resistance **R ≈ 1.36 K/W**

This independently reproduces the earlier Week 4 **≤1.36 K/W** screening requirement. The implication is that natural convection alone would need a relatively large exposed area if the complete 11.043 W were forced through one surface. The real Sentinel package should therefore use parallel paths: direct sensor convection, conduction into the robot chassis/top deck, and a metallic spreader path rather than a sealed stagnant plastic cover.

---

## 6. Verification Checks

1. **Zero-power limit:** as Q → 0, the model returns Tjunction → Tambient.
2. **Area trend:** increasing external area monotonically reduces T_wall and T_junction.
3. **Conductivity trend:** increasing wall conductivity reduces R_wall,cond and cannot increase T_junction.
4. **Churchill–Chu regime check:** all baseline Rayleigh numbers remain far below 10^9, so the laminar natural-convection treatment is appropriate for this screening model.
5. **Week 4 cross-check:** the Sentinel surface-temperature calculation reproduces the previous 1.36 K/W equivalent target.
6. **Physical limitation check:** the high predicted enclosure-wall temperatures show why junction compliance alone cannot be treated as a complete human-proximate product requirement.

---

## 7. Limitations and Validation Path

The largest uncertainty is not the Churchill–Chu equation; it is the **unknown physical heat path inside Fari**. The model does not know the actual processor, PCB copper distribution, heat-spreader geometry, contact pressure, enclosure shape, vents, internal air gaps or user-contact zones. Radiation is omitted, which is conservative for predicted temperature, while assuming a uniform effective convection area may be non-conservative if much of the shell is blocked internally or externally.

Before detailed design release, the model should be replaced or calibrated using:

- the actual compute-module and sensor power measurements;
- measured enclosure dimensions and thermal contact areas;
- manufacturer RθJC / ΨJT data for the selected processor;
- thermocouples on the SoC/package, PCB, spreader and enclosure wall during a full-load soak test;
- an IR image to identify hot spots;
- CFD only if the enclosure contains complex vented or forced internal flow.

The required physical validation experiment is a **steady-state full-power thermal soak in still air at the worst intended ambient**, logging junction proxy temperature and enclosure-wall temperature until temperature rise changes negligibly with time.

---

## 8. Final Design Requirements

1. **Junction temperature:** Tj ≤ 85 °C at 30 °C ambient under the 14.87 W screening budget.
2. **Passive path:** provide a metallic heat-spreader path from compute PCB/module to the enclosure wall.
3. **Effective area:** retain at least **0.045 m²** effective natural-convection area for the selected spreader concept; target more area where packaging permits.
4. **TIM:** use a medium-conductivity or better interface; ultra-high-k TIM is not a substitute for adequate exposed area.
5. **Fins:** reserve external fins as a secondary option if measured junction or wall temperatures exceed target.
6. **Validation:** verify the final enclosure with a steady-state thermal soak using measured hardware power and actual geometry.

---

## References

1. InGen Dynamics Inc., *Mechanical Engineer Internship Program Plan*, Week 5: Robot Electronics Thermal Management Analysis, pp. 10–11.
2. InGen Dynamics Inc., *Mechanical Engineer Internship Concepts Primer*, Section E: Thermal Management, pp. 6–7.
3. `W04_Sensor_Selection_and_Preliminary_Calculations.md`, Week 4 thermal screening: VLP-16 8 W + D435 3.043 W = 11.043 W; equivalent target ≤1.36 K/W.
4. NVIDIA, *Jetson Orin NX Series and Jetson Orin Nano Series Modules Thermal Design Guide*, TDG-11127-001 v1.5, Table 3-12: Orin Nano 4GB 10 W mode total dissipated power 8.87 W, SoC 6.90 W, Rj-c 0.218 °C/W.
5. S. W. Churchill and H. H. S. Chu, “Correlating equations for laminar and turbulent free convection from a vertical plate,” *International Journal of Heat and Mass Transfer*, 1975.
6. Material conductivities and internal contact resistances in this report are preliminary engineering assumptions for sensitivity analysis and must be replaced by selected-material / measured interface data before release.
