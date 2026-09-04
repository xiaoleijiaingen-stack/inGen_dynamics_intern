# W07 — Design Verification Report

**Programme:** InGen Dynamics Mechanical Engineer Internship  
**Intern:** Xiaolei Jia  
**Scope:** Analytical model audit across Phases A–C (Weeks 2–6)  
**Standard:** Rover kinematic & structural standard — geometric model, governing relations, worst-case requirement, verification check  
**Analysis level:** Pre-PDR verification / assumption audit

---

## Executive Finding

**The Phase A–C analytical chain is internally consistent, but the largest remaining non-conservative uncertainty is the Week 3 local structural response under terrain-step loading.** The global beam model gives a credible preliminary cross-member requirement of **\(Z_x \ge 12.37\,cm^3\)** and a candidate global yield FoS of **2.88**, but it excludes local joint stress concentration, fatigue, torsion and welded heat-affected-zone strength reduction. Those effects can change local stress by tens of percent to order unity, so the Week 3 result is suitable for preliminary member sizing but not final structural release.

The Week 2 and Week 6 kinematic models are geometrically self-consistent: the Week 6 nominal case reproduces the Week 2 **48.8° lateral tipping limit** and **3.93 m swept diameter**. Their main uncertainty is real skid-steer slip and the estimated **0.70 m CoM height**. The Week 5 thermal model also reaches a clear design decision — passive cooling is feasible with the selected spreader concept — but its **4.9°C junction-temperature margin** is small enough that a modest hardware-model error could reverse the pass/fail result.

The Week 4 sensor integration calculation is useful as a requirements screen, but CAD/model validation remains open because the SolidWorks assembly was intentionally deferred.

---

## 1. Verification framework

For each model, this report checks:

1. **Key result and physical interpretation**
2. **Modelling assumptions**
3. **Most significant error source**
4. **Conservative or non-conservative error direction**
5. **Order-of-magnitude error estimate**
6. **Named validation path**

A conservative assumption pushes the design toward the safe side. A non-conservative assumption can make performance or strength appear better than it is.

---

## 2. Week 2 — Aido Rover drivetrain, turning and anti-tipping

### Key result

- Counter-rotation gives **0 m centre-path turning radius**.
- The physical body still requires **3.93 m clear swept diameter**.
- Static tipping limits are **60.8° longitudinal** and **48.8° lateral**; lateral governs.
- Nominal ground pressure is **28.4 kPa**, with the original contact-patch uncertainty producing **21.3–42.7 kPa**.

### Assumptions and error direction

The model treats the 4-wheel independent drive as ideal differential/skid-steer kinematics and neglects lateral tyre slip, tyre deformation, suspension compliance, terrain sinkage and payload offset. Track width and wheelbase are estimates, and the CoM height is estimated at **0.70 m**.

The ideal no-slip turning relation is **potentially non-conservative for manoeuvrability**, because real skid-steer scrub/slip can increase or distort the commanded path radius. The CoM-height error can be conservative or non-conservative depending on whether the actual CoM is lower or higher than 0.70 m.

### Error estimate

A useful sensitivity bound is the CoM-height range **0.60–0.80 m** while holding the 1.60 m track fixed:

\[
\theta_{lat}=\tan^{-1}\left(\frac{0.80}{h}\right)
\]

- \(h=0.60\,m\Rightarrow\theta_{lat}\approx53.1^\circ\)
- \(h=0.70\,m\Rightarrow\theta_{lat}=48.8^\circ\)
- \(h=0.80\,m\Rightarrow\theta_{lat}=45.0^\circ\)

Thus, a ±0.10 m CoM error moves the lateral tipping prediction by about **4°**. For turning, a **10–30%** trajectory error is an appropriate preliminary uncertainty band until skid-steer slip is measured; this is an engineering estimate, not a field-derived statistic.

### Existing verification check

The limiting cases are physically correct: equal side speeds give straight motion, one stationary side gives a centre radius of half the track, and equal/opposite side speeds give zero centre-path radius.

### Validation path

Use a GPS/odometry-logged turning test at several commanded left/right wheel-speed ratios on high- and low-friction surfaces. Measure CoM or perform a controlled tilt-table test for the stability limit. Measure actual tyre contact area for ground-pressure closure.

---

## 3. Week 3 — Aido Rover chassis structural analysis

### Key result

The **single-wheel terrain-step impact** governs:

\[
M_{impact}=1.707\,kN\cdot m
\]

\[
Z_{req}=12.37\,cm^3
\]

The preliminary **80 × 40 × 4 mm 6061-T6 RHS** provides \(Z=17.78\,cm^3\) and a global yield FoS of **2.88** under the simplified model.

### Assumptions and error direction

The cross-member is reduced to a global bending member. The model excludes local bracket bending, weld/bolt stress concentration, torsion, fatigue, suspension compliance and chassis-rail interaction. The terrain-step load uses **DAF = 2.0**.

The omitted local effects are **non-conservative**, because they can make peak local stress higher than the beam stress. The DAF selection may be conservative or non-conservative depending on the real suspension stiffness, damping, speed and obstacle profile.

### Error estimate

The dominant uncertainty is not arithmetic; it is the load path. Local stress can plausibly differ from the global beam stress by **tens of percent to order unity**. The governing moment is also directly proportional to DAF, so if a measured event produces DAF = 1.5 or 2.5 rather than 2.0, the impact moment and required section modulus change by approximately **−25% or +25%**, respectively.

### Existing verification check

The half-cross-member cantilever expression was cross-checked against the equivalent simply supported beam calculation for the symmetric flat-ground case. This verifies the global equilibrium formulation.

### Validation path

Run an instrumented terrain-step test with accelerometers and strain gauges at the wheel attachment and cross-member centreline. Build local FEA including suspension brackets, fasteners and welded HAZ allowables. Use the measured acceleration/load history for fatigue analysis.

---

## 4. Week 4 — Sentinel Prime AI sensor integration screening

### Key result

The pre-CAD sensor package gives:

- **1.225 kg** provisional package mass
- **0.275 kg** remaining margin to the 1.50 kg cap
- **73.6 N** design-basis inertial load at the full mass limit under 5g
- **11.043 W** heat load
- \(R_{\theta,eff}\le1.36\,K/W\) screening target for a 50°C surface at 35°C ambient

### Assumptions and error direction

The largest limitation is that the design is still **pre-CAD**. Mounting-structure mass is an allocation, not a mass-properties result, and modal separation/FoV interference are not yet verified.

This is **potentially non-conservative** if the real mount is heavier, taller or more flexible than the allocation.

### Error estimate

The mass margin is only **0.275 kg**. A structure growth of:

- +0.10 kg consumes about **36%** of the remaining margin.
- +0.20 kg consumes about **73%** of the remaining margin.

Resonant amplification cannot be credibly bounded until geometry, stiffness and motor excitation are known.

### Existing verification check

The mass budget is explicitly closed by summation. The 5g inertial load was checked at the full 1.50 kg package limit. The thermal screening target was later independently closed in Week 5: **11.043 W**, 35°C ambient and 50°C surface correspond to approximately **0.124 m²** natural-convection area and **1.36 K/W**, consistent with the Week 4 requirement.

### Validation path

Complete the CAD assembly and use mass properties, FoV/interference checks and modal/stress analysis. Then perform a 5g-equivalent shock/shaker test with cable routing installed.

---

## 5. Week 5 — Fari thermal resistance network

### Key result

At **14.87 W** total enclosure heat and **30°C** ambient:

- Baseline ABS, \(A=0.040\,m^2\): **Tj = 88.5°C** → fails 85°C target
- Aluminium heat spreader at the same external area: **83.6°C** → passes
- Selected spreader + medium-k TIM + \(A\ge0.045\,m^2\): **Tj ≈ 80.1°C**
- Margin to target: **4.9°C**

### Assumptions and error direction

The network uses assumed contact/mount resistances, idealised exposed natural-convection area and a representative compute/sensor power budget. Radiation is neglected.

Neglecting radiation is **conservative** because radiation would provide an additional heat-loss path. However, assuming the full geometric area receives free natural-convection access, or underestimating interface resistance, is **non-conservative**.

### Error estimate

The selected design has only **4.9°C** modelled thermal margin. A **+5°C** prediction error would consume the entire margin. Until actual component placement, contact stack and airflow obstruction are known, a **±5–10°C** preliminary uncertainty band is more appropriate than treating 80.1°C as a release-quality prediction.

### Existing verification check

The computed Rayleigh number remains in the laminar range used by the chosen Churchill–Chu relation. The Week 5 model also reproduces the earlier Sentinel Prime AI thermal screening target, providing an independent carry-over check.

### Validation path

Run a still-air thermal-chamber test at 30°C ambient and the measured full power load. Log junction/board temperature and enclosure-wall thermocouples; use an IR map for surface non-uniformity. Measure the actual TIM/contact stack.

---

## 6. Week 6 — Aido Rover wheelbase-to-track parameter study

### Key result

The one-variable \(L/W\) sweep gives:

\[
1.50\le L/W\le1.79
\]

as the screened feasible range, with **1.55–1.65** recommended for further development. The nominal **1.5625** geometry remains acceptable.

### Assumptions and error direction

The comparison turning case uses \(v_L/v_R=0.5\) because the zero-radius centre-path case is insensitive to track width. Slip is neglected. The **45° lateral stability target** and **R ≤ 2.50 m** manoeuvrability target are explicit Week 6 screening criteria, not published product requirements.

Ignoring slip is **non-conservative for manoeuvrability** if the real rover turns on a larger path than the ideal kinematic model. The stability trend with track width is robust, but its absolute value remains sensitive to CoM height.

### Error estimate

A **10–30%** turning-radius uncertainty band is retained until skid-steer slip is measured. The earlier ±0.10 m CoM sensitivity corresponds to roughly **4°** uncertainty in the lateral tipping threshold.

### Existing verification check

At the nominal \(L/W=1.5625\), the Week 6 model reproduces the Week 2 **48.8° lateral tipping limit** and **3.93 m physical swept diameter**.

### Validation path

Measure turning trajectories at multiple speed ratios, repeat the stability test on a tilt table, and then re-run the Pareto screen using actual deployment-clearance and safety requirements rather than preliminary screening thresholds.

---

## 7. Integrated assumption audit

| Model | Dominant uncertainty | Error direction | Approximate significance | Validation priority |
|---|---|---|---|---|
| Week 2 kinematics | Skid-steer slip / CoM estimate | Mostly non-conservative | ~10–30% turn path; ~4° stability for ±0.10 m CoM | High |
| Week 3 structure | Local load path + DAF | Non-conservative locally | Tens of % to order unity local stress; moment scales linearly with DAF | **Highest** |
| Week 4 sensor integration | Pre-CAD mass/stiffness/modal response | Non-conservative if heavier/flexible | +0.10–0.20 kg consumes 36–73% of mass margin | High |
| Week 5 thermal | Contact resistance / usable convection area | Mixed | ±5–10°C preliminary uncertainty vs 4.9°C margin | **Highest** |
| Week 6 parameter study | Slip + screening thresholds | Mostly non-conservative for turning | ~10–30% turn metric; ~4° CoM sensitivity | Medium–High |

---

## 8. Verification conclusion and next actions

The analytical work is suitable for **pre-PDR concept decisions**, but not for final design release.

**Priority 1 — Structural validation:** replace the Week 3 global-only load path with measured terrain-step acceleration and local FEA/strain data. This addresses the largest non-conservative mechanical uncertainty and the S = 9 structural FMEA mode.

**Priority 2 — Thermal hardware test:** verify the Week 5 spreader concept because the predicted **4.9°C margin** is smaller than the reasonable preliminary model uncertainty.

**Priority 3 — Kinematic/stability test:** measure actual skid-steer turning trajectories and CoM/tilt behaviour, then update the Week 6 Pareto screen.

**Priority 4 — Complete sensor CAD:** close mass properties, FoV, shock stress, modal separation and cable routing that remain open from Week 4.

The strongest aspect of the current analysis chain is internal traceability: Week 6 reproduces Week 2 geometry results, Week 4 carries the Week 3 structural constraint into sensor packaging, and Week 5 independently closes the Week 4 thermal screening target. The main remaining work is therefore not additional hand calculation, but replacing remote-design assumptions with physical or higher-fidelity evidence.
