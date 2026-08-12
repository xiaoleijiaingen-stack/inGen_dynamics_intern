# W04 — Sensor Integration Design Note

**Programme:** InGen Dynamics Mechanical Engineer Internship  
**Intern:** Xiaolei Jia  
**Platform anchor:** Sentinel Prime AI patrol platform, with Aido Rover structural constraints carried forward  
**Deliverable:** Sensor integration design note, CAD intentionally deferred  
**Analysis level:** Preliminary pre-CAD / pre-PDR screening  

---

## Executive Finding

**The reference LiDAR + depth-camera payload is feasible against the Week 4 mass, shock and thermal screening requirements before CAD.** The selected package uses a VLP-16-family 360° LiDAR and an Intel RealSense D435 depth camera. The provisional package mass is **1.225 kg**, leaving **0.275 kg** margin against the **1.50 kg** Week 4 limit. The conservative **5g** inertial design load is **73.6 N** at the full mass limit, and the preliminary heat load is **11.043 W**, requiring an equivalent package-to-ambient resistance of **≤ 1.36 K/W** if the external surface must remain below **50 °C** at **35 °C** ambient.

CAD is skipped in this submission because the SolidWorks licence renewal is not available. This note therefore treats geometry as **CAD-ready requirements**, not as a completed SolidWorks assembly.

---

## 1. Design Objective and Carry-Forward Constraints

Week 4 applies the same discipline used in the Halo Copilot smart-hat project: define the active perception hardware first, then design the mounting concept around **geometry, structure, thermal behaviour and mass budget**. The Halo Copilot method is directly relevant because both systems integrate active sensors into a compact mechanical platform with field-of-view, mass and heat-dissipation constraints.

The sensor platform is anchored to Sentinel Prime AI because it is a patrol/security robot where 360° perception is mechanically important. Aido Rover results from Weeks 2–3 are carried forward as conservative design constraints because its drivetrain and chassis analyses provide the best available numerical basis.

| Carry-forward result | Value used in Week 4 | Design implication |
|---|---:|---|
| Aido Rover centre-path turning radius | 0 m in counter-rotation | Sensor package must not create unnecessary overhang. |
| Aido Rover swept diameter during in-place rotation | 3.93 m | The sensor mast footprint should remain compact and inside the body envelope. |
| Lateral static tipping limit | 48.8° | Added top-side sensor mass should be kept low and close to the centreline. |
| Maximum modelled Rover mass | 435 kg | Sensor mass is treated as part of the full-sensor configuration, not added again as an extra payload. |
| Governing structural case | Single-wheel terrain-step impact | Shock and mass control are the controlling packaging concerns. |
| Cross-member requirement | \(Z_x \geq 12.37\ \mathrm{cm^3}\) | Avoid adding avoidable top-deck mass or high moment-arm loads. |
| Candidate cross-member achieved FoS | 2.88 | Preliminary margin exists, but local sensor-interface strength still needs CAD/FEA or hand checks. |

---

## 2. Component List and Preliminary Mass Budget

**Engineering conclusion.** The sensor payload is acceptable before CAD because the provisional mass budget is **1.225 kg**, which remains **18.3%** below the 1.50 kg limit.

| Component | Mass used | Basis | Function |
|---|---:|---|---|
| VLP-16-family 360° LiDAR | 0.800 kg | Conservative representative value within the Week 4 LiDAR mass range | Surrounding patrol perception and obstacle mapping |
| Intel RealSense D435 depth camera | 0.075 kg | Manufacturer nominal class value used in previous calculation note | Forward depth perception and short-range object geometry |
| Mounting structure allowance | 0.200 kg | Pre-CAD allocation | Base plate, LiDAR ring, camera bracket, standoffs |
| Cables, fasteners and interface allowance | 0.150 kg | Pre-CAD allocation | USB-C, LiDAR power/data, strain relief, M5-class fasteners |
| **Total package budget** | **1.225 kg** | Sum | Within 1.50 kg target |
| **Remaining margin** | **0.275 kg** | 1.500 - 1.225 | 18.3% mass margin |

\[
m_{total}=0.800+0.075+0.200+0.150=1.225\ \mathrm{kg}
\]

\[
m_{margin}=1.500-1.225=0.275\ \mathrm{kg}
\]

**Design requirement:** the final sensor package, including all brackets, cables, fasteners and interface hardware, shall not exceed **1.50 kg**. The CAD-derived structure mass should target **≤ 0.20 kg** to preserve the current margin.

---

## 3. Requirement Set

### 3.1 Geometric Requirements

**Engineering conclusion.** The LiDAR must be the highest local perception component and must have an unobstructed 360° horizontal scan plane. The D435 should sit below the LiDAR scan plane with a preliminary **15° downward tilt**.

| Requirement | Target | Rationale | Verification method |
|---|---:|---|---|
| LiDAR horizontal FoV | 360° unobstructed | Avoid blind sectors during patrol | CAD scan-plane cylinder / visual section check |
| LiDAR mounting hierarchy | Highest local component | Keep brackets and cable loops below scan plane | CAD side view and envelope check |
| Depth camera direction | Forward-facing | Patrol direction short-range depth | Assembly datum and bracket angle |
| Depth camera tilt | -15° downward preliminary | Improves near-ground obstacle visibility | CAD angle dimension and field-of-view sketch |
| Cable route | Rearward/downward below scan plane | Avoid LiDAR occlusion and cable snag | Harness path review |
| Serviceability | Remove each sensor independently | Maintainability and modularity | Assembly sequence review |

**CAD-ready concept dimensions, deferred:**

| Feature | Reference dimension | Source of dimension |
|---|---:|---|
| Base plate footprint | 220 × 160 mm | Compact footprint below body envelope |
| LiDAR mount ring | OD 130 mm / ID 105 mm / thickness 8 mm | Fits VLP-16-class outer diameter with clearance |
| Standoff height | 45 mm | Raises LiDAR scan plane above camera and cable route |
| Camera bracket | 110 × 32 × 3 mm, -15° | Fits D435-class camera width and tilt requirement |
| Generic chassis bolt pattern | 180 × 120 mm, M5 | Placeholder only; replace with measured chassis data |

These dimensions are **not claimed as completed CAD**. They are the requirement-driven skeleton for the first SolidWorks model after the licence is renewed.

### 3.2 Structural Requirements

**Engineering conclusion.** The conservative structural screening load is **73.6 N** at the full 1.50 kg package limit under a 5g shock case. Current estimated package mass produces **60.1 N**, so the full-mass case should be used for later bracket sizing.

\[
F=ma=m(5g)
\]

\[
F_{limit}=1.50\times5\times9.81=73.6\ \mathrm{N}
\]

\[
F_{budget}=1.225\times5\times9.81=60.1\ \mathrm{N}
\]

| Structural check | Requirement | Current status |
|---|---:|---|
| Package shock survival | 5g equivalent-static load | Screening load calculated |
| Design-basis inertial load | 73.6 N | Use for later bracket and interface sizing |
| Current-budget inertial load | 60.1 N | Expected if 1.225 kg budget holds |
| Resonance avoidance | First housing mode ≥ 20% away from motor excitation frequency | Deferred until CAD geometry and motor RPM are known |
| Local bracket stress | No yielding under shock case | Deferred until material, section and fastener layout are fixed |

Because the Week 3 Rover cross-member result is governed by dynamic terrain-step loading, the sensor interface should avoid tall, flexible brackets and unnecessary mass high above the chassis. A low base plate plus raised LiDAR ring is preferred over a tall decorative cover.

### 3.3 Thermal Requirements

**Engineering conclusion.** The preliminary heat load is **11.043 W**. To keep the external housing surface below **50 °C** at **35 °C** ambient using a single equivalent path, the package would require \(R_{\theta,eff}\leq1.36\ \mathrm{K/W}\). Week 5 should replace this screening model with a multi-path thermal resistance network.

| Heat source | Power / TDP used | Comment |
|---|---:|---|
| VLP-16-family LiDAR | 8.000 W | Approximate normal operating power used as heat load |
| Intel RealSense D435 | 3.043 W | TDP used as heat-load input |
| **Total heat load** | **11.043 W** | Preliminary Week 4 thermal design load |

\[
Q_{total}=8.000+3.043=11.043\ \mathrm{W}
\]

\[
\Delta T_{allow}=50-35=15\ ^\circ\mathrm{C}
\]

\[
R_{\theta,eff}\leq\frac{15}{11.043}=1.36\ \mathrm{K/W}
\]

**Thermal design target:** use thermally conductive mounting material where practical, avoid enclosing the LiDAR in a stagnant plastic cover, and leave a direct thermal path from sensor bases into the top deck or aluminium spreader. This is a screening recommendation only; material selection should be finalised in Week 5 after the thermal resistance network.

### 3.4 Mass Budget Requirements

**Engineering conclusion.** Mass is the tightest Week 4 requirement because the sensor payload already consumes **81.7%** of the 1.50 kg limit.

| Mass item | Target / result | Status |
|---|---:|---|
| Total package cap | ≤ 1.50 kg | Requirement |
| Current provisional package | 1.225 kg | Pass before CAD |
| Current remaining margin | 0.275 kg | Moderate margin |
| Mechanical/interface allowance | 0.350 kg | Must include brackets, cables, fasteners, adapter |
| CAD mass target for mounting structure | ≤ 0.200 kg | Required to keep current budget |

A protective shell should not be added unless mass is recovered through pocketing, thinner sections, or mixed materials. The design should prioritise a stiff, open, serviceable frame instead of cosmetic enclosure surfacing.

---

## 4. Design Rationale by Major Feature

| Feature | Rationale | Requirement served | Current verification status |
|---|---|---|---|
| Raised LiDAR ring | Keeps 360° scan plane clear of brackets and cable loops | Geometry / FoV | Requirement defined; CAD check deferred |
| Low base plate | Keeps mass close to chassis and reduces overturning moment | Mass / stability / structure | Mass allocation defined |
| Forward D435 bracket at -15° | Gives near-ground forward depth view for patrol navigation | Geometry / sensing | Angle target defined |
| Rearward/downward cable exit | Keeps harness below LiDAR plane and reduces snag risk | Geometry / reliability | Routing requirement defined |
| Modular sensor interfaces | Allows LiDAR or camera replacement without reworking chassis adapter | Serviceability | Assembly sequence deferred |
| Thermally conductive mount path | Provides preliminary path for 11.043 W heat load | Thermal | Week 5 network required |

---

## 5. Requirements Compliance Summary

| Requirement category | Result | Status | Reason |
|---|---|---|---|
| Geometry / FoV | 360° LiDAR plane and -15° camera tilt defined | **Green before CAD** | Requirements are clear and can be converted to reference geometry. |
| Structure / shock | 73.6 N design-basis 5g load defined | **Green before CAD** | Load case is quantified; detailed stress remains CAD-dependent. |
| Thermal | 11.043 W heat load and ≤1.36 K/W target defined | **Amber** | Screening target exists; actual temperature depends on Week 5 resistance network. |
| Mass | 1.225 kg against 1.50 kg cap | **Green / Amber** | Passes at allocation level, but CAD mass properties may consume margin. |
| Resonance | Avoid motor excitation by ≥20% | **Open** | Requires final geometry, boundary conditions and motor RPM. |
| CAD assembly | SolidWorks assembly not produced | **Deferred** | Licence renewal blocker; no CAD completion claimed. |

---

## 6. Failure Modes to Carry into Week 7 FMEA

| Failure mode | Physical mechanism | Effect on platform | Preliminary mitigation |
|---|---|---|---|
| LiDAR scan obstruction | Bracket, cable loop or chassis feature intersects scan plane | Blind sectors during patrol | Keep all structure and cable exits below scan plane; CAD scan-plane check |
| Camera bracket fatigue | Repeated terrain shock causes bracket crack or tilt drift | Depth-camera calibration loss and perception error | Short bracket, filleted bends, 5g load sizing, later modal check |
| Cable snag / connector load | Cable routed into rotating or exposed area | Sensor dropout or damaged connector | Rearward/downward cable route, strain relief, minimum bend radius |
| Thermal heat soak | 11.043 W heat load accumulates in poorly conductive enclosure | High surface temperature or sensor throttling | Aluminium spreader path; Week 5 thermal network |
| Interface mismatch | Placeholder bolt pattern does not match actual chassis | Package cannot be mounted without rework | Replace generic 180 × 120 mm pattern with measured/OEM geometry |
| Resonance near motor excitation | Housing natural frequency close to motor/chassis vibration frequency | Amplified vibration and sensor misalignment | Modal check after CAD; target ≥20% frequency separation |

---

## 7. Deferred CAD Scope

The following items are intentionally deferred because geometry is not yet available and SolidWorks access is blocked:

- Native SolidWorks part files and assembly file.
- Final bracket bending stress and tip deflection.
- Fastener shear, tension, bearing and tear-out loads.
- Local stress concentration and fatigue checks.
- First natural frequency and mode-shape check.
- Exact mass properties and centre of gravity.
- Final LiDAR scan-plane interference check.

**CAD resumption plan:** build a parametric skeleton first, not a cosmetic model: base plate, LiDAR ring, camera bracket, chassis adapter and cable reference curves. The first CAD milestone should verify requirement compliance, not surface styling.

---

## 8. Decision Summary

| Decision / result | Value | Current status |
|---|---:|---|
| Reference LiDAR | VLP-16-family 360° LiDAR | Selected for Week 4 study |
| Reference depth camera | Intel RealSense D435 | Selected |
| Preliminary package mass | 1.225 kg | Within 1.50 kg target |
| Mass margin | 0.275 kg / 18.3% | Preliminary; CAD mass pending |
| Conservative shock load | 73.6 N at 1.50 kg | Use for later sizing |
| Current-budget shock load | 60.1 N | Expected if present allocation holds |
| Preliminary thermal load | 11.043 W | Week 5 model input |
| Thermal-resistance screening target | ≤ 1.36 K/W | Week 5 validation required |
| Governing requirement category | Mass + thermal | Mass controls packaging margin; thermal controls material path |
| CAD status | Deferred | Not claimed complete |
