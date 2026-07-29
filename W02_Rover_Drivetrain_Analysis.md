# W02 Rover Drive-Train Analysis

## Executive Findings

The Aido Rover can achieve a zero **centre-path** turning radius through counter-rotation of the left and right wheel sets. However, its 3.45 m by 1.88 m body still sweeps a radius of **1.96 m**, requiring approximately **3.93 m of clear diameter** for a complete in-place rotation.

Using the estimated 2.50 m wheelbase, 1.60 m track width and 0.70 m centre-of-mass height, the theoretical static tipping limits are **60.8 degrees longitudinally** and **48.8 degrees laterally**. The lateral direction governs, but both limits remain above the product specification of 30 degrees sustained and 35 degrees momentary. This indicates that traction, wheel slip, suspension travel and terrain irregularity are more likely to constrain the stated grade capability than rigid-body static tipping.

At the maximum stated 435 kg configuration and an assumed tyre contact patch of 0.25 m by 0.15 m per wheel, the nominal flat-ground pressure is **28.4 kPa**. Because tyre contact geometry is not provided, the plausible pressure range is **21.3-42.7 kPa**.

## 1. Source Data and Assumptions

### Confirmed product data

| Parameter | Value |
|---|---:|
| Drive configuration | Four-wheel independent electric drive |
| Overall dimensions | 3.45 m x 1.88 m x 1.71 m |
| Unloaded mass | 395 kg |
| Maximum stated mass with full sensor configuration | 435 kg |
| Ground clearance | 0.25 m |
| Cruise speed | 0.8-1.2 m/s |
| Maximum speed | 1.5 m/s |
| Stated turning radius | 0 m |
| Sustained incline | 30 degrees |
| Momentary incline | 35 degrees |

### Estimated model inputs

| Parameter | Value | Basis |
|---|---:|---|
| Wheelbase | 2.50 m | 72% of overall length |
| Track width | 1.60 m | 85% of overall width |
| Wheel diameter | 0.65 m | Scale and ground-clearance estimate |
| CoM height | 0.70 m | Preliminary mass-distribution estimate |
| Contact patch per wheel | 0.0375 m^2 | 0.25 m x 0.15 m assumed patch |

The model treats the Rover as an equivalent differential-drive/skid-steer vehicle. It neglects lateral slip, tyre deformation, suspension compliance and terrain sinkage. The 150 kg payload-capacity statement is not added to the 435 kg full-sensor configuration because the relationship between those values is unclear.

## 2. ICR and Turning Radius

The right-side speed is normalised to 1.0 m/s and the left/right speed ratio is varied. Equal wheel-set speeds give straight motion. A stationary left side gives a centre turning radius equal to half the track width, or 0.80 m. Equal and opposite side speeds give zero centre speed and a zero centre-path turning radius.

| vL/vR | Centre speed (m/s) | Yaw rate (rad/s) | Ideal centre radius (m) |
|---:|---:|---:|---:|
| -1.00 | 0.000 | 1.250 | 0.000 |
| -0.75 | 0.125 | 1.094 | 0.114 |
| -0.50 | 0.250 | 0.938 | 0.267 |
| -0.25 | 0.375 | 0.781 | 0.480 |
| 0.00 | 0.500 | 0.625 | 0.800 |
| 0.25 | 0.625 | 0.469 | 1.333 |
| 0.50 | 0.750 | 0.312 | 2.400 |
| 0.75 | 0.875 | 0.156 | 5.600 |
| 0.90 | 0.950 | 0.062 | 15.200 |

The stated zero-metre turning radius refers to the path of the vehicle centre. It does not mean the platform needs zero space. During in-place rotation, the furthest body corner is approximately 1.96 m from the vehicle centre, producing a swept diameter of 3.93 m.

## 3. Static Anti-Tipping

The theoretical longitudinal tipping limit is **60.8 degrees**. The theoretical lateral limit is lower at **48.8 degrees**, so lateral stability governs the rigid-body model.

At a 30-degree longitudinal grade, the downhill wheels carry approximately **1223 N each**, while the uphill wheels carry approximately **625 N each**. On a 30-degree lateral slope, the downhill wheels carry approximately **1391 N each**, while the uphill wheels carry only **457 N each**.

| Slope | Long. downhill wheel | Long. uphill wheel | Lateral downhill wheel | Lateral uphill wheel |
|---:|---:|---:|---:|---:|
| 0 deg | 1067 N | 1067 N | 1067 N | 1067 N |
| 15 deg | 1185 N | 876 N | 1272 N | 789 N |
| 30 deg | 1223 N | 625 N | 1391 N | 457 N |
| 35 deg | 1217 N | 531 N | 1409 N | 338 N |

The static calculation does not prove that the Rover can safely operate at 48.8 degrees. It only shows that, under the rigid-body assumptions, geometric tipping should not occur before that angle. At the stated sustained grade of 30 degrees, the ideal traction requirement is approximately **mu = 0.577**. At 35 degrees it rises to approximately **mu = 0.700**. Wet grass, mud, sand and loose gravel may therefore cause slip before the static tipping boundary is reached.

## 4. Ground Pressure

On flat ground, the nominal wheel load is **1067 N per wheel**. With the assumed 0.0375 m^2 contact patch, the average ground pressure is **28.4 kPa**.

At a 30-degree longitudinal grade, the estimated wheel pressures are **32.6 kPa downhill** and **16.7 kPa uphill**. On a 30-degree lateral slope, they are **37.1 kPa downhill** and **12.2 kPa uphill**.

Because no tyre size, inflation pressure or measured contact-patch data are available, ground pressure has higher uncertainty than the turning and static-stability results. The report therefore includes a sensitivity range from 0.025 to 0.050 m^2 per wheel.

## 5. Verification Checks

1. **Straight-line limit:** as vL approaches vR, yaw rate approaches zero and turning radius approaches infinity.
2. **Counter-rotation limit:** when vL equals -vR, centre speed and centre turning radius both become zero.
3. **Flat-ground equilibrium:** the four wheel reactions sum to the total weight of 4267 N.
4. **Tipping limit:** at the calculated tipping angle, the uphill axle or side reaction approaches zero.
5. **Specification comparison:** the model reproduces the stated zero centre-path turning capability, and the 30-degree sustained grade lies below both theoretical static tipping limits.

## 6. Operational Implications

- Zero-radius centre rotation still requires approximately **3.93 m** of clear circular space because of the body dimensions.
- Lateral slope operation is more critical than straight uphill travel because track width is smaller than wheelbase.
- At a 30-degree lateral slope, the uphill side retains only about **24.7%** of the total normal load, increasing sensitivity to local terrain loss and suspension motion.
- The stated 30-degree capability is more likely governed by traction and terrain interaction than by static rigid-body tipping.
- The ground-pressure result should be updated when tyre width, inflation pressure and measured contact area become available.

## 7. Limitations

The analysis is a preliminary planar model. It excludes skid-steer scrub, mecanum roller geometry, dynamic acceleration, braking, suspension articulation, terrain steps, tyre compliance, soil sinkage and an offset payload. Wheelbase, track width, wheel diameter, CoM height and contact area remain estimated values. The model should be updated when dimensioned chassis and mass-property data become available.
