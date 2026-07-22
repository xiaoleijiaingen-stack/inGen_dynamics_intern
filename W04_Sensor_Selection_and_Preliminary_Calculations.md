# 1. Objective and Design Basis

**Engineering conclusion.** The selected reference payload is a 360-degree LiDAR from the Ouster/Velodyne VLP 16 family plus an Intel RealSense D435 depth camera. The combination satisfies the Week 4 functional intent: long-range surrounding perception plus forward depth perception. Before CAD, the main quantified checks are package mass, 5g shock load, and a first-order thermal budget.

The internship plan requires a long-range LiDAR, a depth camera, cable-management provisions, and four requirement categories: geometric, structural, thermal, and mass. It also sets a total sensor-plus-housing target of 1.5 kg and gives a 5g terrain-step shock case as an example structural load. The 50 °C surface target at 35 °C ambient is retained as the preliminary thermal requirement.

## 1.1 Packaging Logic Before CAD

| Category | Preliminary requirement | Basis | Status in this note |
|---|---|---|---|
| Geometry | LiDAR: unobstructed 360° horizontal scan; camera: forward-facing, preliminary 15° downward tilt | Week 4 plan + sensor function | Defined; CAD verification deferred |
| Structure | 5g equivalent-static screening load | Week 4 plan example load case | Calculated |
| Thermal | Surface target < 50 °C at 35 °C ambient | Week 4 plan | First-order heat-load screening calculated |
| Mass | Sensor package + housing ≤ 1.50 kg | Week 4 plan | Preliminary budget calculated |
| Vibration | Avoid resonance with motor excitation | Week 4 plan | Requires final geometry and excitation data; deferred |

> **Important assumption boundary**
>
> The VLP 16 calculation mass is set to 0.80 kg as a conservative representative design value within the 0.5-0.8 kg range specified by the internship plan. It is not presented as a current vendor-certified mass. Final procurement and CAD work must use the exact selected hardware variant and its current manufacturer drawing.

```text
VLP 16 FAMILY / 360° LiDAR
Highest local component
Keep scan plane clear

          ↓ Downward packaging and cable routing

D435 DEPTH CAMERA
Forward-facing with preliminary 15° downward tilt

          ↓ Downward packaging and cable routing

COMMON MOUNTING STRUCTURE
Geometry to be modelled later

          ↓

SENTINEL PRIME AI CHASSIS INTERFACE
Final dimensions pending
```

# 2. Equipment Selection

## 2.1 Long-Range LiDAR: Ouster / Velodyne VLP 16 Family

**Selection rationale.** The VLP 16 family is retained because the internship plan explicitly identifies it as the reference class, while the current Ouster product page confirms 360-degree horizontal field of view and a 40-degree vertical field of view. The manufacturer user manual states approximately 8 W power draw in normal operation. These characteristics match the patrol-robot requirement for surrounding perception without making the Week 4 concept dependent on proprietary InGen hardware data.

| Parameter | Value used | How it is used in this study |
|---|---:|---|
| Horizontal field of view | 360° | Drives unobstructed scan-plane requirement |
| Vertical field of view | 40° | Context only; not used in current calculations |
| Normal-operation power | Approx. 8 W | Conservative thermal load input |
| Calculation mass | 0.80 kg design assumption | Mass and shock calculations; final vendor mass pending |
| Mechanical envelope | Deferred to final vendor CAD/drawing | No housing geometry is frozen in this note |

## 2.2 Forward Depth Camera: Intel RealSense D435

**Selection rationale.** The D435 is compact, light, and intended for robotic depth perception. The current D400 family datasheet gives nominal dimensions of 90 × 25 × 25 mm and nominal mass of 75 g. At maximum operating mode, the datasheet lists total electrical power of 3.403 W and thermal design power of 3.043 W for the D435/D435-family camera. For thermal screening, the TDP value is the more appropriate heat-load input.

| Parameter | Value used | How it is used in this study |
|---|---:|---|
| Nominal dimensions | 90 × 25 × 25 mm | Packaging reference for later CAD |
| Nominal mass | 75 g | Mass and shock calculations |
| Electrical interface | USB Type-C | Cable-management requirement |
| Max operating-mode electrical power | 3.403 W | Electrical budget reference |
| Max operating-mode TDP | 3.043 W | Thermal heat-load input |

## 2.3 Why This Pair Is Mechanically Useful

- The LiDAR provides surrounding range perception; the D435 provides dense forward depth information.
- The packaging hierarchy is clear: the LiDAR must remain the highest local component, while the camera and cable routes stay below the horizontal scan plane.
- Each sensor can be replaced without redesigning the complete patrol-chassis interface.
- Both sensors have published technical documentation, allowing sourced data to be separated from design assumptions.

# 3. Preliminary Mass Budget

**Engineering conclusion.** A provisional package budget of 1.225 kg leaves 0.275 kg, or 18.3% of the 1.50 kg limit, for uncertainty and later design refinement. The result is a budget allocation, not a CAD-derived mass property.

| Item | Mass used | Basis | Design note |
|---|---:|---|---|
| VLP 16 family LiDAR | 0.800 kg | Conservative design assumption within Week 4 plan range | Replace with exact procured variant mass |
| Intel RealSense D435 | 0.075 kg | Manufacturer nominal mass | Published value; nominal tolerance applies |
| Mounting structure allowance | 0.200 kg | Pre-CAD engineering allocation | Replace with CAD mass properties |
| Cables, fasteners, and interface allowance | 0.150 kg | Pre-CAD engineering allocation | Includes uncertainty in harness/interface hardware |
| **Total** | **1.225 kg** | Calculated | Preliminary package budget |
| **Margin to 1.50 kg limit** | **0.275 kg** | 1.500 - 1.225 | **18.3% of total limit** |

\[
m_{\text{total}} = 0.800 + 0.075 + 0.200 + 0.150 = 1.225\ \text{kg}
\]

\[
m_{\text{margin}} = 1.500 - 1.225 = 0.275\ \text{kg}
\]

> **Interpretation**
>
> The current result says the concept is feasible at the allocation level, not that a particular SolidWorks assembly has already passed the mass target. The 0.350 kg mechanical/interface allowance is the maximum combined budget available to the mounting structure, cables, fasteners, and interface hardware under the present assumptions.

## 3.1 5g Equivalent-Static Shock Load

The Week 4 plan suggests a 5g terrain-step shock case. Two loads are useful: a conservative design-basis load at the full 1.50 kg limit and the current provisional load at the 1.225 kg package budget.

\[
F = ma = m(5g)
\]

\[
F_{\text{limit}} = 1.50 \times 5 \times 9.81 = 73.6\ \text{N}
\]

\[
F_{\text{budget}} = 1.225 \times 5 \times 9.81 = 60.1\ \text{N}
\]

| Load case | Equivalent inertial load | Use |
|---|---:|---|
| Maximum allowed package mass, 1.50 kg | 73.6 N | Recommended conservative load for later bracket/interface sizing |
| Current provisional package budget, 1.225 kg | 60.1 N | Expected load if the present mass allocation is maintained |

**Deferred geometry-dependent checks.** Bending stress, bolt-load distribution, local bearing stress, bracket deflection, and factor of safety cannot be finalised responsibly until the actual mounting geometry, material, fasteners, and boundary conditions are defined in CAD.

# 4. Preliminary Thermal Screening

**Engineering conclusion.** Using 8 W for the LiDAR and 3.043 W D435 TDP, the preliminary heat load is 11.043 W. With the selected 50 °C surface-temperature target at 35 °C ambient, a single-path equivalent thermal resistance would need to be about 1.36 K/W or lower. This is a screening target only; Week 5 should replace it with a multi-path thermal resistance network.

| Source | Thermal input | Basis | Comment |
|---|---:|---|---|
| VLP 16 family LiDAR | 8.000 W | Manufacturer manual: approximate normal-operation power | Used conservatively as heat load |
| RealSense D435 | 3.043 W | Manufacturer D400 datasheet: maximum operating-mode TDP | Preferred over 3.403 W electrical input for heat estimate |
| **Total** | **11.043 W** | Sum | Preliminary thermal design load |

\[
Q_{\text{total}} = 8.000 + 3.043 = 11.043\ \text{W}
\]

\[
\Delta T_{\text{allow}} = 50 - 35 = 15\ ^\circ\text{C}
\]

\[
R_{\theta,\text{eff}} \leq \frac{\Delta T_{\text{allow}}}{Q_{\text{total}}}
\]

\[
R_{\theta,\text{eff}} \leq \frac{15}{11.043} = 1.36\ \text{K/W}
\]

## 4.1 What the 1.36 K/W Target Means

- It is not a measured thermal resistance of the future housing.
- It is the maximum equivalent package-to-ambient resistance for a simplified single-path model that would limit temperature rise to 15 °C at 11.043 W.
- The real system will have parallel heat paths: direct convection from sensor surfaces, conduction into the mount, conduction into the robot chassis, radiation, and cable conduction.
- The Week 5 model should separate the LiDAR and camera heat paths instead of treating the complete payload as one lumped heat source.

> **Thermal design implication**
>
> The current calculations justify keeping the future mounting structure thermally conductive where practical, but they do not yet prove that an aluminium plate is required or sufficient. Material selection should follow the Week 5 resistance-network result rather than be fixed now.

# 5. Cable-Management and Integration Requirements

| Requirement | Reason | Verification later |
|---|---|---|
| Keep all structural members and cable loops below the LiDAR horizontal scan plane | Avoid blind sectors and self-occlusion | CAD section view + scan-plane reference geometry |
| Route the D435 USB Type-C cable rearward/downward with strain relief | Reduce connector load and snag risk | Cable route in assembly + minimum bend radius from selected cable |
| Provide serviceable sensor removal without removing the complete chassis interface | Modularity and maintenance | Assembly-sequence review |
| Separate final sensor-interface dimensions from the generic chassis adapter | Avoid treating estimated InGen geometry as production data | Measured/OEM chassis geometry before fabrication |

# 6. Assumptions, Limitations, and Deferred Work

| Item | Current treatment | Risk if wrong | Required closure action |
|---|---|---|---|
| LiDAR exact variant mass | 0.80 kg design assumption | Mass margin could increase or decrease | Confirm exact procured part number and current datasheet |
| Mounting structure mass | 0.20 kg allocation | Actual CAD may exceed budget | Use SolidWorks mass properties after geometry is built |
| Cable/interface mass | 0.15 kg allocation | Underestimated harness/interface hardware could consume margin | Create detailed BOM and obtain vendor masses |
| 5g shock case | Equivalent-static screening load | Real transient load spectrum may differ | Obtain platform acceleration data or define a validated shock spectrum |
| Thermal model | Single equivalent-resistance screening | Distributed heat paths are not represented | Build Week 5 resistance network |
| Resonance | Not calculated | Bracket may coincide with motor/chassis excitation | Define CAD, constraints, and excitation frequencies; perform modal analysis |
| Chassis-interface geometry | Not frozen | Concept may not fit the actual robot | Replace with measured or OEM geometry |

## 6.1 Calculations Intentionally Deferred Until CAD

- Bracket bending stress and tip deflection.
- Fastener shear, tension, and bearing loads.
- Local stress concentration and factor of safety.
- First natural frequency and mode shapes.
- Exact mass properties and centre of gravity.
- Final field-of-view clearance based on actual sensor envelopes and chassis geometry.

> **Recommended next step**
>
> Build only a simple parametric SolidWorks skeleton after the sensor variant and chassis interface are confirmed. The first CAD milestone should be requirement verification, not cosmetic surfacing.

# 7. Decision Summary

**Overall conclusion.** The selected VLP 16-family LiDAR and D435 camera form a technically appropriate reference payload for the Week 4 sensor-integration study. The pre-CAD calculations show a feasible mass allocation, define a conservative 73.6 N structural screening load, and establish an 11.043 W thermal design load. The next legitimate engineering step is to freeze the exact sensor variant and chassis interface before geometry-dependent structural and modal calculations are performed.

| Decision / result | Value | Current status |
|---|---:|---|
| Reference LiDAR | Ouster/Velodyne VLP 16 family | Selected for Week 4 study |
| Reference depth camera | Intel RealSense D435 | Selected |
| Preliminary package budget | 1.225 kg | Within 1.50 kg target |
| Mass margin | 0.275 kg (18.3%) | Preliminary; CAD mass pending |
| 5g conservative design load | 73.6 N at 1.50 kg limit | Use for later structural sizing |
| Current-budget 5g load | 60.1 N | Expected under present allocation |
| Preliminary thermal load | 11.043 W | Based on LiDAR power + D435 TDP |
| Equivalent thermal-resistance target | ≤ 1.36 K/W | Screening result; Week 5 model pending |
| CAD / modal / detailed stress | Deferred | Not claimed complete |

# References

1. InGen Dynamics Inc., *Internship Program Plan, Mechanical Engineer Intern - 8-Week Remote Program*, Week 4 requirements and deliverables, pp. 8-9.
2. Ouster, "VLP 16" product page, current product information accessed 15 July 2026: 360° horizontal FOV and 40° vertical FOV.
3. Ouster / Velodyne, *VLP-16 User Manual*, Rev. F, normal-operation power approximately 8 W.
4. Intel / RealSense, *D400 Series Product Family Datasheet*, October 2024, Table 3-52: D435 nominal 90 × 25 × 25 mm and 75 g; Table 7-8: D435-family 3.403 W electrical power and 3.043 W TDP at maximum operating mode.
5. Intel, *RealSense Depth Camera D435 Product Specifications*, USB Type-C interface and 90 × 25 × 25 mm module dimensions.



- https://ouster.com/products/hardware/vlp-16
- https://data.ouster.io/downloads/velodyne/user-manual/vlp-16-user-manual-revf.pdf
- https://www.intel.com/content/www/us/en/products/sku/128255/intel-realsense-depth-camera-d435/specifications.html
- https://realsenseai.com/wp-content/uploads/2024/10/Intel-RealSense-D400-Series-Datasheet-October-2024.pdf
