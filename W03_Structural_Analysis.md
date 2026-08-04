# W03 — Aido Rover Structural Analysis

**Programme:** InGen Dynamics Mechanical Engineer Internship  
**Intern:** Xiaolei Jia  
**Platform anchor:** Aido Rover — chassis structural loading  
**Analysis level:** Preliminary hand-calculation / pre-PDR screening  
**Units:** SI unless stated otherwise

## Executive Findings

**The single-wheel terrain-step impact governs the preliminary chassis cross-member design.** Using the Week 2 maximum configuration mass of **435 kg**, an estimated **1.60 m track width**, and a **2.0 dynamic amplification factor**, the governing limit bending moment is **1.707 kN·m**. With a selected yield safety factor of **2.0**, the cross-member requires a minimum elastic section modulus of:

\[
\boxed{Z_{\mathrm{req}} \geq 12.37\ \mathrm{cm^3}}
\]

A preliminary **6061-T6 aluminium rectangular hollow section (RHS), 80 mm × 40 mm × 4 mm**, oriented with the 80 mm dimension vertical, provides \(Z = 17.78\ \mathrm{cm^3}\). Under the simplified beam model, it achieves a yield factor of safety of **2.88** in the governing impact case.

The flat-ground static case requires \(Z_{\mathrm{req}} = 4.64\ \mathrm{cm^3}\), while the 35° lateral-slope case requires \(Z_{\mathrm{req}} = 8.17\ \mathrm{cm^3}\). The impact case governs because the terrain step doubles the nominal wheel reaction before the uncertainty safety factor is applied.

> **Design requirement:** the selected cross-member shall provide \(Z_x \geq 12.4\ \mathrm{cm^3}\) about its strong bending axis, and the impacted wheel attachment load path shall resist a factored vertical load of at least **4.27 kN**.

---

## 1. Platform Inputs, Load Path and Assumptions

The Week 3 model carries forward the same geometry and mass assumptions used in the Week 2 Aido Rover drive-train analysis.

| Parameter | Value | Status / basis |
|---|---:|---|
| Maximum modelled mass, \(m\) | 435 kg | Confirmed maximum full-sensor configuration used in Week 2 |
| Vehicle weight, \(W=mg\) | 4,267 N | Calculated using \(g=9.81\ \mathrm{m/s^2}\) |
| Track width, \(B\) | 1.60 m | Week 2 estimate |
| Half cross-member length, \(l=B/2\) | 0.80 m | Derived |
| Centre-of-mass height, \(h\) | 0.70 m | Week 2 estimate |
| Maximum operational slope | 35° | Momentary product specification used in Week 2 |
| Material | 6061-T6 aluminium | Preliminary cross-member material |
| Yield strength, \(\sigma_y\) | 276 MPa | Kaiser Aluminum typical T6/T651 value |
| Elastic modulus, \(E\) | 68.3 GPa | Kaiser Aluminum typical value |

### 1.1 Cross-member idealisation

The analysed member is a transverse chassis cross-member connecting the left and right wheel or suspension load paths. Because the detailed rail spacing and suspension pickup geometry are unavailable, each half of the cross-member is treated as a cantilever cut at the vehicle centreline:

```text
vehicle centreline                       wheel / suspension station
        ||-----------------------------------------↑ R
        ||<--------------- 0.80 m ---------------->|
        fixed cut                         vertical wheel reaction
```

The centreline bending moment for one side is therefore:

\[
M = Rl
\tag{1}
\]

For the flat-ground symmetric case, this is equivalent to a full simply supported beam of span \(B\) carrying the axle load \(W/2\) at mid-span:

\[
M_{\max}=\frac{(W/2)B}{4}=\frac{WB}{8}=Rl
\tag{2}
\]

This equivalence is used as the hand-calculation verification check.

### 1.2 Main modelling assumptions

1. The chassis is a rigid body and the centre of mass is centred longitudinally and laterally.
2. Front and rear axles each carry half of the vehicle weight on flat ground.
3. The cross-member response is linear elastic and dominated by strong-axis bending.
4. Torsion, local bracket bending, weld stress concentration, bolt bearing, fatigue, suspension compliance and chassis-rail interaction are excluded.
5. The impact case doubles the **nominal static load on the impacted wheel**; it does not assume complete transfer of the entire axle load to one wheel.
6. The 6061-T6 strength is a parent-material value. A welded design must use reduced heat-affected-zone allowables and be checked again.

---

## 2. Design Method and Safety-Factor Basis

The required section modulus is obtained from elastic bending:

\[
\sigma_{\max}=\frac{M}{Z}
\tag{3}
\]

\[
Z_{\mathrm{req}}=\frac{SF\cdot M_{\mathrm{limit}}}{\sigma_y}
\tag{4}
\]

NASA-STD-5001B is used as the **methodology reference** because it explicitly defines yield design load as the product of limit load and yield factor of safety, and requires factored stress to remain below the material allowable. It is not being claimed as a mobile-robot-specific standard. Because this is an unvalidated remote preliminary model, the selected factors are deliberately higher than the minimum metallic yield factors listed in that standard.

| Load case | Additional load factor | Yield safety factor | Rationale |
|---|---:|---:|---|
| Static full load | 1.0 | 1.5 | Well-defined gravity load, but geometry and load distribution remain estimated |
| Single-wheel step impact | DAF = 2.0 | 2.0 | Sudden load plus uncertain suspension and local load path |
| Maximum-slope / tipping case | 1.0 | 2.0 | Strong load redistribution and stability consequence |

The internship plan names ISO 2631 as an example. ISO 2631-1 concerns **human exposure to whole-body vibration**, not chassis strength or structural safety-factor selection. It is therefore not used to prescribe the cross-member safety factors in this memo.

For the terrain-step screening case, \(DAF=2.0\) is the classical undamped linear-elastic response to a suddenly applied step load: the peak response reaches twice the corresponding static response. A measured terrain profile and suspension model are required to replace this preliminary factor.

---

## 3. Load Case 1 — Maximum Mass on Flat Ground

### 3.1 Load-case definition

The 435 kg Rover is stationary on level ground. The vehicle is supported at four wheel stations, with equal reactions because the centre of mass is assumed centred.

\[
R_{\mathrm{flat}}=\frac{W}{4}
=\frac{435(9.81)}{4}
=1066.8\ \mathrm{N}
\tag{5}
\]

The centreline moment in one half cross-member is:

\[
M_{\mathrm{static}}=R_{\mathrm{flat}}l
=1066.8(0.80)
=853.5\ \mathrm{N\,m}
\tag{6}
\]

Using \(SF=1.5\):

\[
Z_{\mathrm{req,static}}
=\frac{1.5(853.5)}{276\times10^6}
=4.638\times10^{-6}\ \mathrm{m^3}
=\boxed{4.64\ \mathrm{cm^3}}
\tag{7}
\]

**Static design requirement:** the cross-member shall provide \(Z_x\geq4.64\ \mathrm{cm^3}\), and each wheel load path shall resist at least \(1.5R_{\mathrm{flat}}=1.60\ \mathrm{kN}\) vertically.

---

## 4. Load Case 2 — Single-Wheel Terrain-Step Impact

### 4.1 Load-case definition

One wheel strikes a terrain step while the Rover is operating at maximum mass. The preliminary impact model applies a dynamic amplification factor of 2.0 to the nominal static wheel reaction:

\[
R_{\mathrm{impact}}=DAF\cdot R_{\mathrm{flat}}
=2.0(1066.8)
=2133.7\ \mathrm{N}
\tag{8}
\]

The corresponding limit bending moment is:

\[
M_{\mathrm{impact}}=R_{\mathrm{impact}}l
=2133.7(0.80)
=1706.9\ \mathrm{N\,m}
\tag{9}
\]

Using \(SF=2.0\):

\[
Z_{\mathrm{req,impact}}
=\frac{2.0(1706.9)}{276\times10^6}
=12.369\times10^{-6}\ \mathrm{m^3}
=\boxed{12.37\ \mathrm{cm^3}}
\tag{10}
\]

The factored wheel attachment load is:

\[
F_{\mathrm{design,impact}}
=SF\cdot R_{\mathrm{impact}}
=2.0(2133.7)
=\boxed{4.27\ \mathrm{kN}}
\tag{11}
\]

**Impact design requirement:** the cross-member shall provide \(Z_x\geq12.37\ \mathrm{cm^3}\), and the impacted suspension or wheel bracket, fasteners and local cross-member wall shall transfer a minimum factored vertical load of 4.27 kN without yielding.

This is the governing global bending case. It does not verify local wall crippling, bolt tear-out, weld fatigue or torsional response from an off-axis wheel force.

---

## 5. Load Case 3 — Maximum Lateral Slope at Maximum Mass

### 5.1 Load-case definition

The Rover is stationary at the 35° momentary operational slope with maximum mass. Lateral slope is used because Week 2 showed that lateral stability governs over longitudinal stability.

For a rigid body with centred CoM, the downhill and uphill wheel reactions are:

\[
R_{\mathrm{down}}
=\frac{W}{4}\cos\theta
+\frac{Wh}{2B}\sin\theta
\tag{12}
\]

\[
R_{\mathrm{up}}
=\frac{W}{4}\cos\theta
-\frac{Wh}{2B}\sin\theta
\tag{13}
\]

At \(\theta=35^\circ\):

\[
R_{\mathrm{down}}=1409.3\ \mathrm{N},\qquad
R_{\mathrm{up}}=338.5\ \mathrm{N}
\tag{14}
\]

The downhill half cross-member governs:

\[
M_{\mathrm{slope}}=R_{\mathrm{down}}l
=1409.3(0.80)
=1127.5\ \mathrm{N\,m}
\tag{15}
\]

Using \(SF=2.0\):

\[
Z_{\mathrm{req,slope}}
=\frac{2.0(1127.5)}{276\times10^6}
=8.170\times10^{-6}\ \mathrm{m^3}
=\boxed{8.17\ \mathrm{cm^3}}
\tag{16}
\]

**Slope design requirement:** the cross-member shall provide \(Z_x\geq8.17\ \mathrm{cm^3}\), and the downhill wheel attachment shall resist a factored vertical load of at least \(2.82\ \mathrm{kN}\).

The uphill wheel retains only 338 N of normal force. This small reaction makes the result sensitive to local terrain loss, suspension articulation and an off-centre payload.

---

## 6. Candidate Cross-Section Check

A preliminary 6061-T6 RHS is checked with:

- overall height \(H=80\ \mathrm{mm}\)
- overall width \(b=40\ \mathrm{mm}\)
- wall thickness \(t=4\ \mathrm{mm}\)
- 80 mm dimension oriented vertically

The second moment of area and elastic section modulus are:

\[
I_x=\frac{bH^3-(b-2t)(H-2t)^3}{12}
=7.113\times10^{-7}\ \mathrm{m^4}
\tag{17}
\]

\[
Z_x=\frac{I_x}{H/2}
=17.783\times10^{-6}\ \mathrm{m^3}
=\boxed{17.78\ \mathrm{cm^3}}
\tag{18}
\]

| Load case | Limit wheel reaction | Limit moment | Required \(SF\) | \(Z_{\mathrm{req}}\) | Stress in 80×40×4 RHS | Achieved yield FoS | End deflection* |
|---|---:|---:|---:|---:|---:|---:|---:|
| Static flat ground | 1.067 kN | 0.853 kN·m | 1.5 | 4.64 cm³ | 48.0 MPa | 5.75 | 3.75 mm |
| Single-wheel impact | 2.134 kN | 1.707 kN·m | 2.0 | **12.37 cm³** | 96.0 MPa | **2.88** | 7.50 mm |
| 35° lateral slope | 1.409 kN | 1.127 kN·m | 2.0 | 8.17 cm³ | 63.4 MPa | 4.35 | 4.95 mm |

\*The deflection estimate uses \(\delta=Rl^3/(3EI)\) for the same half-member cantilever idealisation. No formal alignment or stiffness limit was supplied, so deflection is reported rather than used as a pass/fail criterion.

The candidate RHS passes the three **global elastic bending** checks. The dynamic case retains approximately 43.8% positive margin relative to the selected factor-of-safety requirement:

\[
MS=\frac{\sigma_y}{SF\,\sigma_{\max}}-1
=\frac{276}{2.0(96.0)}-1
=0.438
\tag{19}
\]

---

## 7. Verification Checks

1. **Flat-ground force equilibrium**

\[
4R_{\mathrm{flat}}=4(1066.8)=4267.2\ \mathrm{N}\approx W
\]

2. **Independent full-span beam cross-check**

\[
M_{\max}=\frac{(W/2)B}{4}
=\frac{(4267.35/2)(1.60)}{4}
=853.5\ \mathrm{N\,m}
\]

This matches the half-member result \(R_{\mathrm{flat}}l=853.5\ \mathrm{N\,m}\).

3. **Slope normal-force equilibrium**

\[
2(R_{\mathrm{down}}+R_{\mathrm{up}})
=3495.6\ \mathrm{N}
\]

\[
W\cos35^\circ=3495.6\ \mathrm{N}
\]

4. **Tipping-limit behaviour**

Using the Week 2 lateral tipping limit \(\theta_{\mathrm{tip}}=\tan^{-1}[(B/2)/h]=48.8^\circ\), Equation (13) drives the uphill reaction to approximately zero, as required by the static tipping condition.

5. **Section verification**

The candidate \(Z_x=17.78\ \mathrm{cm^3}\) exceeds the governing requirement \(12.37\ \mathrm{cm^3}\) by 43.8%.

---

## 8. Final Design Requirements and Limitations

### 8.1 Preliminary requirements

1. **Cross-member section modulus:** \(Z_x\geq12.4\ \mathrm{cm^3}\) about the strong axis.
2. **Recommended preliminary section:** 6061-T6 RHS, 80 mm × 40 mm × 4 mm, 80 mm vertical, subject to joint and fatigue verification.
3. **Impact attachment load:** wheel/suspension attachment path shall resist at least 4.27 kN factored vertical load.
4. **Slope attachment load:** downhill attachment shall resist at least 2.82 kN factored vertical load at 35°.
5. **Stiffness follow-up:** the predicted 7.5 mm impact deflection shall be checked against suspension alignment, sensor stability and tyre-clearance requirements.
6. **Validation:** perform a detailed chassis FEA using measured geometry and suspension pickup locations, followed by a controlled terrain-step test with wheel-force or strain-gauge instrumentation.

### 8.2 Limitations

This memo is a preliminary global beam calculation, not a released chassis design. The governing uncertainty is the actual load path between the wheel module, suspension, cross-member and longitudinal rails. The model also excludes:

- combined bending and torsion from off-axis wheel forces;
- braking and longitudinal impact loads;
- local stress concentration around holes, brackets and weld toes;
- welded 6061-T6 heat-affected-zone strength reduction;
- fatigue under repeated patrol cycles;
- nonlinear suspension and tyre response;
- an off-centre or moving payload;
- chassis-shell contribution and load sharing among multiple cross-members.

The cross-section recommendation must therefore be treated as a minimum screening result pending detailed CAD, FEA and physical validation.



