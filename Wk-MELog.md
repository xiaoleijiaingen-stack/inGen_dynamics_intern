# Mechanical Engineering Log

## Week 2

## What was modelled

This week I built a planar drive-train model for Aido Rover using the confirmed four-wheel independent-drive architecture and the preliminary geometry defined during Week 1. The model used a 2.50 m wheelbase, 1.60 m track width, 0.70 m centre-of-mass height and the maximum stated 435 kg sensor configuration. I evaluated the ideal instantaneous centre of rotation and turning radius as the left/right wheel-speed ratio changed, then calculated longitudinal and lateral static tipping limits, slope-dependent wheel reactions and ground-pressure sensitivity.

## What the results revealed

Counter-rotating the left and right wheel sets gives a zero centre-path turning radius, which is consistent with the product specification. However, the body still sweeps a 3.93 m diameter during a complete in-place rotation. The theoretical static tipping limits are 60.8 degrees longitudinally and 48.8 degrees laterally, so lateral stability governs. Both values exceed the stated 30-degree sustained grade. This suggests that traction, wheel slip, suspension articulation and terrain irregularity are more likely to limit deployment than rigid-body static tipping. At a 30-degree lateral slope, each uphill wheel carries only about 457 N, compared with 1,391 N on each downhill wheel.

## Next question

The largest uncertainty is the tyre-ground contact model. Tyre width, pressure, stiffness and measured contact area are unavailable, so the nominal 28.4 kPa ground-pressure result is only a first estimate. The next question is what tyre and suspension data are required to determine whether the 30-degree grade is traction-limited or stability-limited on wet grass, mud and loose gravel.

## Week 3

## What I modelled

I converted the Week 2 Aido Rover mass and geometry assumptions into a preliminary transverse chassis cross-member model. The Rover was evaluated at the 435 kg maximum configuration, with a 1.60 m track width and a 0.70 m centre-of-mass height. I treated each half of the cross-member as a 0.80 m cantilever between the chassis centreline and the wheel or suspension load path. Three required cases were analysed: maximum mass on flat ground, a single-wheel terrain-step impact with a 2.0 dynamic amplification factor, and maximum-mass operation on the 35° momentary lateral slope. I then converted each limit bending moment into a minimum section modulus using 6061-T6 aluminium and explicit yield safety factors.

## What the analysis revealed

The single-wheel impact case governed the design. It produced a limit bending moment of 1.707 kN·m and required a minimum section modulus of 12.37 cm³. The static and slope cases required 4.64 cm³ and 8.17 cm³, respectively. A preliminary 80 mm × 40 mm × 4 mm 6061-T6 rectangular hollow section provides 17.78 cm³ and achieves a calculated yield factor of safety of 2.88 in the impact case. The impact case governs physically because the terrain step doubles the nominal wheel reaction before the uncertainty safety factor is applied.

## Next engineering question

The largest uncertainty is the real suspension-to-chassis load path. The assumed centreline cut may overestimate or underestimate local bending depending on the longitudinal rail spacing, bracket offset and load sharing between cross-members. Dimensioned CAD, suspension pickup locations and either FEA or strain-gauge data from a controlled terrain-step test are needed before this preliminary section can be released.

## Week 4   

## What I modelled

I converted the Week 2–3 Aido Rover results into packaging requirements for a Sentinel Prime AI patrol sensor platform. The selected reference payload is a VLP-16-family 360° LiDAR plus an Intel RealSense D435 depth camera. Because SolidWorks access is blocked by the licence renewal issue, I did not claim CAD completion; instead, I built a pre-CAD design note with quantified geometry, structural, thermal and mass requirements. The main calculations were the preliminary package mass, the 5g equivalent-static shock load and the first-order thermal screening target. I also defined CAD-ready reference dimensions for the later base plate, LiDAR ring, camera bracket and chassis interface.

## What the analysis revealed

The sensor package is feasible before CAD but mass and thermal margin are the controlling constraints. The provisional package mass is 1.225 kg, leaving 0.275 kg margin against the 1.50 kg target. The conservative 5g inertial design load is 73.6 N at the full mass limit, while the current 1.225 kg budget gives 60.1 N. The combined LiDAR and D435 heat load is 11.043 W, which implies an equivalent thermal-resistance target of no more than 1.36 K/W to keep the surface below 50 °C at 35 °C ambient.

## Next engineering question

The requirement category that most constrained the design is mass, followed closely by thermal management. The largest open question is whether the final SolidWorks geometry can keep the mounting structure below the 0.20 kg allocation while still providing enough stiffness and a usable thermal path. Once SolidWorks is available again, the first CAD step should be a requirement-verification skeleton, not cosmetic modelling.

## Week 5

## What I modelled

This week I built a lumped thermal-resistance model for Fari's compact electronics enclosure, using a representative 14.87 W embedded-electronics heat budget and the programme's worst indoor ambient of 30 °C. The model retains the required junction-to-case, case-to-PCB, PCB-to-enclosure and enclosure-to-ambient paths, with the external convection coefficient calculated from the Churchill–Chu vertical-plate correlation. I then varied effective enclosure area from 0.03 to 0.12 m² and compared ABS, 6061 aluminium and 304 stainless steel wall conductivity. I also screened an aluminium heat spreader, an external fin array and TIM conductivity.

## What it revealed

The most important result is that external natural-convection area becomes the dominant constraint once a reasonable conductive path exists. At 0.040 m² effective area, the baseline ABS case predicts 88.5 °C, slightly above the 85 °C junction target, while adding an aluminium heat-spreader path reduces the prediction to 83.6 °C. The selected spreader + medium-k TIM concept with 0.045 m² area predicts 80.1 °C, so passive cooling is feasible in the current screening model.

The key scaling difference from my RVACS dissertation is that the robot enclosure is centimetre-scale and operates at Ra of order 10^6, so the relevant external flow is laminar natural convection rather than the turbulent/forced-convection regime that justified CFD turbulence modelling in the reactor problem.

