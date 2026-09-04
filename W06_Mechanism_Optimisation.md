# W06_Mechanism_Optimisation
## Aido Rover Wheelbase-to-Track Ratio Parameter Study

### Engineering conclusion

The Aido Rover's current wheelbase-to-track ratio of **L/W = 1.5625** lies inside a screened Pareto-feasible range of approximately **1.50 to 1.79**. Within this range, the rover preserves a representative centre-path turning radius no larger than its 2.50 m wheelbase while maintaining at least a **45° lateral static tipping limit**, which provides a 10° geometric reserve above the 35° momentary terrain case carried forward from Week 2. The existing **L = 2.50 m, W = 1.60 m** geometry therefore remains a defensible baseline rather than requiring a major chassis-width change.

A preferred design band of **L/W ≈ 1.55–1.65** is recommended for further development. It retains approximately **47.3–49.0°** lateral static tipping capability while giving a representative turning radius of approximately **2.27–2.42 m** for the comparison manoeuvre used in this study. The current nominal ratio, 1.5625, sits near the stability-favouring end of this band.

---

## 1. Objective and selected parameter

Week 6 requires a one-variable-at-a-time parameter study for Aido Rover. The selected parameter is the **wheelbase-to-track ratio**

\[
\rho = \frac{L}{W}
\]

swept over the programme-defined range **0.8 ≤ L/W ≤ 2.0**.

The wheelbase is held fixed at **L = 2.50 m** and the track width is varied as

\[
W = \frac{L}{\rho}.
\]

This choice directly extends the Week-2 drivetrain model and produces a physically meaningful tradeoff: a narrower track improves manoeuvrability but reduces lateral anti-tipping margin, while a wider track improves stability but increases the turning envelope.

### Carry-forward baseline from Week 2

| Quantity | Value |
|---|---:|
| Drive configuration | 4-wheel independent / skid-steer |
| Wheelbase, L | 2.50 m |
| Nominal track width, W | 1.60 m |
| Nominal L/W | 1.5625 |
| CoM height, h | 0.70 m |
| Overall chassis size | 3.45 m × 1.88 m |
| Lateral static tipping limit | 48.8° |
| Longitudinal static tipping limit | 60.8° |
| Intended terrain | 30° sustained; 35° momentary |
| Zero-centre-path turn | R = 0 m under equal/opposite wheel motion |
| Physical swept diameter at nominal geometry | 3.93 m |

Only **track width W** is changed in this Week-6 sweep. Wheelbase, CoM height, body length, drive type and operating assumptions are held constant.

---

## 2. Governing relations

### 2.1 Representative turning radius

For ideal differential/skid-steer planar kinematics,

\[
R = \frac{W}{2}\frac{v_R+v_L}{v_R-v_L}.
\]

The Week-2 minimum centre-path radius is zero during equal and opposite wheel motion, so it cannot distinguish one L/W value from another. For the Week-6 comparison only, a representative non-zero steering condition is introduced:

\[
\lambda = \frac{v_L}{v_R} = 0.5.
\]

Therefore,

\[
R = \frac{W}{2}\frac{1+0.5}{1-0.5} = 1.5W = \frac{3.75}{\rho}.
\]

This is a **comparison metric**, not a new claimed vehicle operating limit. Real skid-steer slip is neglected, consistent with the ideal Week-2 planar model.

### 2.2 Lateral static tipping limit

The lateral tipping threshold occurs when the CoM projection reaches the side edge of the support polygon:

\[
\tan(\theta_{lat})=\frac{W/2}{h}.
\]

With **h = 0.70 m** and **W = L/ρ**,

\[
\theta_{lat} = \tan^{-1}\left(\frac{L}{2h\rho}\right).
\]

Increasing L/W narrows the track and therefore reduces lateral static stability.

### 2.3 Physical swept diameter in a zero-radius turn

The Week-2 model distinguished zero **centre-path** turning radius from the finite envelope of the physical body. To retain that distinction, the body swept diameter is also tracked:

\[
D_{swept}=2\sqrt{\left(\frac{L_{body}}{2}\right)^2+
\left(\frac{W_{body}}{2}\right)^2}.
\]

At the nominal geometry the body is 0.28 m wider than the track, so the sweep assumes the same 0.14 m overhang per side:

\[
W_{body} = W + 0.28.
\]

This reproduces the Week-2 nominal swept diameter of approximately **3.93 m**, providing the required verification check.

---

## 3. Parameter sweep results

| L/W | Track W (m) | R at vL/vR=0.5 (m) | Lateral tip limit (°) | Swept diameter (m) |
|---:|---:|---:|---:|---:|
| 0.80 | 3.125 | 4.688 | 65.9 | 4.847 |
| 1.00 | 2.500 | 3.750 | 60.8 | 4.431 |
| 1.20 | 2.083 | 3.125 | 56.1 | 4.182 |
| 1.40 | 1.786 | 2.679 | 51.9 | 4.021 |
| 1.50 | 1.667 | 2.500 | 50.0 | 3.961 |
| **1.5625 nominal** | **1.600** | **2.400** | **48.8** | **3.929** |
| 1.60 | 1.562 | 2.344 | 48.1 | 3.911 |
| 1.786 | 1.400 | 2.100 | 45.0 | 3.837 |
| 1.80 | 1.389 | 2.083 | 44.8 | 3.832 |
| 2.00 | 1.250 | 1.875 | 41.8 | 3.774 |

![Turning radius sweep](W06_TurningRadius_vs_Ratio.png)

**Figure 1.** Increasing L/W narrows the track and reduces the representative centre-path turning radius.

![Tipping sweep](W06_TippingLimit_vs_Ratio.png)

**Figure 2.** Increasing L/W reduces lateral static tipping capability because the support-polygon half-width becomes smaller.

![Swept diameter sweep](W06_SweptDiameter_vs_Ratio.png)

**Figure 3.** A narrower track also reduces the physical swept diameter during an ideal zero-radius turn.

---

## 4. Pareto-feasible range

The internship plan does not provide numerical Week-6 acceptance thresholds, so two explicit **screening criteria** are introduced for this study rather than presented as InGen specifications:

1. **Manoeuvrability screen:** representative centre-path turning radius at vL/vR = 0.5 must not exceed the 2.50 m wheelbase.

\[
R \le 2.50\;m \Rightarrow \rho \ge 1.50.
\]

2. **Lateral stability screen:** static lateral tipping limit must be at least 45°. This is chosen as a preliminary design target to retain a 10° geometric reserve above the Week-2 35° momentary terrain case.

\[
\theta_{lat} \ge 45^\circ \Rightarrow \rho \le 1.786.
\]

Combining the two constraints gives

\[
\boxed{1.50 \le L/W \le 1.79}.
\]

This is the **screened Pareto-feasible range**: below 1.50 the rover becomes unnecessarily wide and the representative turning radius exceeds one wheelbase; above 1.79 the narrowing track reduces the lateral tipping threshold below the selected 45° preliminary target.

The nominal ratio **1.5625** satisfies both constraints and reproduces the Week-2 48.8° lateral tipping result.

---

## 5. Design recommendation

Retain the current geometry as the baseline and target **L/W ≈ 1.55–1.65** in future packaging iterations.

At the lower extreme of the complete study range (**L/W = 0.8**), the 3.125 m track produces excellent static stability (65.9° lateral tipping limit) but a very large 4.688 m representative turning radius and a 4.847 m physical swept diameter. The rover becomes unnecessarily wide for patrol manoeuvring.

At the upper extreme (**L/W = 2.0**), the 1.25 m track improves manoeuvrability to a 1.875 m representative turning radius and a 3.774 m swept diameter, but the lateral static tipping limit falls to 41.8°. That leaves only 6.8° of geometric margin above the 35° momentary terrain assumption.

The nominal **L/W = 1.5625** therefore represents a sensible compromise: it gives a 2.40 m representative turn radius, reproduces the 48.8° lateral tipping result, and preserves the previously validated 3.93 m zero-radius swept diameter. Moving modestly toward **1.60–1.65** could improve manoeuvrability without materially sacrificing static stability, but ratios above approximately **1.79** should not be adopted without either lowering the CoM or accepting a smaller lateral stability reserve.

---

## 6. Assumptions, limitations and verification

- The rover is treated as a rigid body with a fixed CoM height of 0.70 m.
- Only one design variable, L/W, is changed; wheelbase remains 2.50 m.
- Track width changes are assumed not to alter mass, suspension geometry or CoM height.
- The skid-steer turning model neglects lateral tyre/ground slip.
- The vL/vR = 0.5 steering condition is introduced only to compare geometries because the zero-radius centre-path case is insensitive to track width.
- The 45° tipping target and R ≤ 2.50 m manoeuvrability target are Week-6 screening criteria, not published InGen requirements.
- The body-overhang assumption is held at 0.14 m per side to estimate swept diameter.

**Verification check:** at the nominal L/W = 2.50/1.60 = 1.5625, the parameter model returns **48.8° lateral tipping limit** and **3.93 m swept diameter**, matching the Week-2 carry-forward results. This confirms that the Week-6 sweep is geometrically consistent with the earlier model.

**Recommended physical validation:** measure actual turning trajectories for several commanded left/right wheel-speed ratios on high- and low-friction surfaces, and perform a controlled tilt-table test to establish the true lateral tipping threshold and effective CoM height.
