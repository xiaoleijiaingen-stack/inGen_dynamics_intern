# W07 — Failure Mode Analysis

**Programme:** InGen Dynamics Mechanical Engineer Internship  
**Intern:** Xiaolei Jia  
**Primary platform anchor:** Aido Rover — outdoor patrol chassis and drivetrain  
**Secondary platform anchor:** Fari — human-proximate companion robot  
**Method:** Programme FMEA framework using Severity (S), Occurrence (O), Detection (D) and RPN = S × O × D  
**Analysis level:** Preliminary pre-PDR screening

---

## Executive Finding

**Environmental sealing is the highest-ranked Aido Rover mechanical reliability risk in this preliminary FMEA, with an initial RPN of 336.** The failure mode is loss of enclosure/cable-entry sealing followed by water or debris ingress, which can produce corrosion, intermittent connections, degraded perception/compute, and mission loss. The recommended mitigation is a combined sealing-and-detection package: sealed cable glands or double-lip gasket geometry, drainage/weep paths, corrosion-resistant hardware, ingress testing, and moisture/self-test monitoring. Under the post-mitigation screening scores used here, its RPN falls to **72**.

The **chassis cross-member fatigue/crack mode has S = 9**, so it receives a separate high-severity review even though its RPN is lower than the environmental-sealing mode. This follows the programme requirement that any failure with **S ≥ 9** be flagged independently of RPN.

For Fari, both selected human-proximate failure modes have **S ≥ 9**. Their RPN values are not the only decision criterion because the operational consequence includes possible contact with an elderly user.

---

## 1. Scoring approach

The internship plan requires five Aido Rover failure modes spanning different subsystems and a two-mode Fari supplement. The programme primer defines:

- **Severity (S):** system consequence, 1–10.
- **Occurrence (O):** expected frequency in the operating environment, 1–10.
- **Detection (D):** difficulty of detecting the failure before a critical consequence, 1–10; higher is worse.
- **RPN:** \(RPN=S\times O\times D\).

The scores below are **engineering screening judgements**, not field-derived reliability statistics. No InGen fleet failure database or hardware test data is available in the remote programme. The relative ranking is therefore more defensible than the absolute number.

---

## 2. Aido Rover FMEA — five mechanical failure modes

| Subsystem                                     | Failure mode                                                                               | Effect                                                                                              |   S |   O |   D |   RPN |
|:----------------------------------------------|:-------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|----:|----:|----:|------:|
| Environmental sealing / electronics enclosure | Enclosure gasket or cable-entry seal loses compression, allowing water/debris ingress      | Corrosion or short/intermittent connections; degraded perception/compute and possible mission loss  |   8 |   6 |   7 |   336 |
| Drivetrain                                    | Wheel bearing seizes from water/debris ingress and lubricant contamination                 | High rolling resistance or locked wheel; yaw error, motor overload, degraded or lost mobility       |   8 |   6 |   6 |   288 |
| Chassis structure                             | Cross-member or suspension-interface fatigue crack initiates at local stress concentration | Loss of wheel alignment/stiffness; progressive structural failure; possible immobilisation          |   9 |   4 |   7 |   252 |
| Sensor mounting                               | LiDAR/camera bracket loosens or cracks under 5g shock or resonant vibration                | Sensor misalignment, partial FoV loss, degraded localisation/perception, possible sensor detachment |   6 |   5 |   6 |   180 |
| Suspension                                    | Suspension bottoms out or mount/fastener loosens under repeated terrain-step excitation    | Higher-than-modelled chassis shock, loss of ride control, secondary damage to wheel/sensor mounts   |   7 |   5 |   5 |   175 |

### 2.1 Rank 1 — Environmental sealing / electronics enclosure

**Finding:** Loss of gasket or cable-entry sealing gives the highest initial RPN, **336**, because Aido Rover's outdoor duty raises contamination occurrence while water ingress can remain hidden until corrosion or intermittent electrical behaviour appears.

**Physical mechanism:** rain, splash, mud, grit, cable motion or ageing reduces seal compression or opens a leakage path. Moisture/debris enters the enclosure and attacks connectors, electronics interfaces or sensor wiring.

**Mitigation:** use sealed glands or a double-lip gasket, provide a deliberate drainage/weep path, avoid water traps, select corrosion-resistant fasteners, perform ingress testing, and add moisture/self-test monitoring where practical.

**Post-mitigation screening:** S remains 8 because the consequence is unchanged, but O is reduced from 6 to 3 and D from 7 to 3:

\[
RPN_{after}=8\times3\times3=\boxed{72}
\]

---

## 3. Mitigation summary

| Subsystem                                     |   RPN | Mitigation                                                                                                                                             |   S_after |   O_after |   D_after |   RPN_after |
|:----------------------------------------------|------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|----------:|----------:|------------:|
| Environmental sealing / electronics enclosure |   336 | Double-lip gasket or sealed cable glands, drainage/weep path, vent strategy, corrosion-resistant hardware, ingress test, moisture/self-test monitoring |         8 |         3 |         3 |          72 |
| Drivetrain                                    |   288 | Sealed bearing, labyrinth shield, drainage, service interval, motor-current/temperature trend monitoring                                               |         8 |         3 |         3 |          72 |
| Chassis structure                             |   252 | Local FEA/fatigue check, gusset/load-path refinement, welded-HAZ allowable, NDT/inspection points, strain validation                                   |         9 |         2 |         4 |          72 |
| Sensor mounting                               |   180 | Positive fastener retention, dowel/location feature, first-mode separation ≥20% from excitation, cable strain relief, shaker/modal validation          |         6 |         2 |         3 |          36 |
| Suspension                                    |   175 | Bump stop and travel margin, locking fasteners, preload marks, suspension travel measurement, measured DAF                                             |         7 |         3 |         3 |          63 |

The mitigation objective is not to reduce Severity by assumption. Most mitigations act on **Occurrence** and **Detection**: prevent the physical mechanism or detect degradation earlier.

---

## 4. High-severity review independent of RPN

The chassis structural mode has **S = 9**:

> **Cross-member or suspension-interface fatigue crack initiates at a local stress concentration.**

The Week 3 global beam calculation produced a governing impact requirement of \(Z_x \ge 12.37\,cm^3\) and a preliminary candidate global yield FoS of 2.88, but that model explicitly excludes local weld/bolt stress concentration, fatigue and torsion. Therefore, the S = 9 structural mode remains open until local FEA/fatigue analysis or physical strain/inspection validation is completed.

---

## 5. Fari human-proximate FMEA supplement

| Subsystem                                       | Failure mode                                                                         | Effect                                                                                        |   S |   O |   D |   RPN |
|:------------------------------------------------|:-------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------|----:|----:|----:|------:|
| Mobility / wheel module                         | Drive wheel or caster mechanically jams while operating next to a user               | Unexpected stop/yaw or loss of manoeuvrability near an elderly user; collision or fall hazard |  10 |   3 |   5 |   150 |
| Human-proximate enclosure / mechanism interface | Cover, bracket or fastener loosens and creates an exposed pinch/sharp-edge condition | User contact injury or snagging during close-proximity interaction                            |   9 |   4 |   4 |   144 |

Both Fari modes receive elevated Severity because the platform operates close to an elderly user.

### 5.1 Fari high-severity interpretation

- **Wheel/caster jam:** S = 10 because an unexpected stop or yaw near a person can create a collision or fall hazard even if the mechanism itself is inexpensive to repair.
- **Loose cover/bracket/fastener:** S = 9 because an exposed sharp edge or pinch interface can directly injure a nearby user.

For both modes, post-mitigation Severity stays high; the strategy is to reduce occurrence and improve detection.

| Subsystem                                       |   RPN | Mitigation                                                                                                           |   RPN_after |
|:------------------------------------------------|------:|:---------------------------------------------------------------------------------------------------------------------|------------:|
| Mobility / wheel module                         |   150 | Low-force speed limit, current/torque anomaly detection, guarded wheel geometry, sealed bearing, periodic inspection |          40 |
| Human-proximate enclosure / mechanism interface |   144 | Captive fasteners, rounded guarded interfaces, thread retention, service inspection checklist, pull/retention test   |          36 |

---

## 6. FMEA limitations and next validation steps

1. Occurrence scores are not based on InGen field-return statistics.
2. Detection scores assume only generic sensing/inspection capability; the actual diagnostic architecture is unknown.
3. RPN is used for prioritisation, but high-Severity modes are reviewed separately.
4. The analysis covers five representative Aido Rover mechanical subsystems, not a complete part-level FMECA.
5. The highest-value next evidence would be: ingress-test results, wheel-bearing environmental qualification, measured terrain-step accelerations, suspension travel logs, modal/shaker data for the sensor mount, and local chassis fatigue/strain data.

**Week 7 design action:** close the environmental-sealing mode first, while keeping the S = 9 chassis-fatigue mode under independent structural review.
