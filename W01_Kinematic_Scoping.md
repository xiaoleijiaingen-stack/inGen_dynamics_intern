# W01_Kinematic_Scoping — Aido Rover

## 1. Purpose and Scope

This document defines the drive configuration, principal geometric parameters, intended terrain gradient, preliminary centre-of-mass height, and explicit geometric assumptions for Aido Rover.

The purpose is to establish a consistent mechanical description of the platform using the detailed internal product specification. Confirmed product values are distinguished from geometric estimates. Where the specification does not provide a dimension directly, a preliminary value is estimated from the overall platform dimensions and typical packaging proportions of a four-wheel outdoor autonomous vehicle.

This document is limited to platform definition and kinematic scoping. It does not contain detailed calculations, simulation results, or structural verification.

## 2. Confirmed Platform Configuration

Aido Rover is an autonomous outdoor inspection and security robot designed for multi-terrain operation. The platform uses a four-wheel independent electric-drive architecture rather than a single-wheel or dynamically balanced configuration.

Each wheel has:

- A dedicated brushless hub motor.
- Independent suspension.
- Independent torque control.
- Terrain-adaptive torque distribution.

Steering is achieved through differential torque vectoring between the four wheels. The platform supports skid-steer or mecanum-style in-place rotation and lateral crab movement for confined access.

The confirmed drive configuration is summarised below.

| Item | Confirmed Configuration |
|---|---|
| Number of wheels | 4 |
| Drive type | Four-wheel independent electric drive |
| Motor arrangement | One dedicated brushless hub motor per wheel |
| Suspension | Independent suspension at each wheel |
| Steering method | Differential torque vectoring |
| Minimum stated turning radius | 0 m |
| Special manoeuvring capability | In-place rotation and lateral crab movement |
| Terrain control | Wheel-slip detection and asymmetric torque redistribution |

The independent-wheel architecture is mechanically appropriate for outdoor inspection because it allows the controller to redistribute torque when the wheels experience different terrain conditions. For example, one wheel may contact wet grass while another contacts gravel or hard pavement.

## 3. Confirmed Overall Dimensions and Mass

The detailed product specification provides the following platform-level dimensions and mass values.

| Parameter | Confirmed Value |
|---|---:|
| Overall length | 3.45 m |
| Overall width | 1.88 m |
| Overall height | 1.71 m |
| Unloaded operating mass | 395 kg |
| Maximum mass with full sensor payload | 435 kg |
| Additional sensor payload capacity | 150 kg |
| Ground clearance | 0.25 m |
| Patrol cruise speed | 0.8–1.2 m/s |
| Maximum open-terrain speed | 1.5 m/s |

The overall dimensions correspond to a large unmanned ground vehicle rather than a compact indoor service robot. The width is intended to remain compatible with standard double-gate access, while the 250 mm ground clearance supports operation over rocks, roots, kerbs, and mud ruts.

## 4. Wheelbase Estimate

The detailed specification provides the overall platform length but does not state the distance between the front and rear wheel centrelines. A preliminary wheelbase must therefore be estimated.

The nominal wheelbase is estimated as:

**Estimated wheelbase: 2.50 m**

This value is approximately 72% of the Rover’s 3.45 m overall length. The remaining length provides approximately 0.95 m of combined front and rear overhang for body panels, impact structures, sensor packaging, environmental sealing, and approach clearance.

A reasonable preliminary range is:

**Estimated wheelbase range: 2.35–2.65 m**

The 2.50 m value should be used as the nominal scoping dimension until a dimensioned chassis drawing or measured prototype value becomes available.

## 5. Track Width Estimate

The specification provides an overall platform width of 1.88 m but does not state the distance between the left and right wheel centrelines.

The nominal track width is estimated as:

**Estimated track width: 1.60 m**

This value is approximately 85% of the overall platform width. The remaining width allows for wheel width, suspension movement, side panels, protective bodywork, and clearance between the tyre sidewalls and the external enclosure.

A reasonable preliminary range is:

**Estimated track-width range: 1.50–1.70 m**

The 1.60 m value represents the lateral distance between the left and right wheel-centre planes rather than the total external body width.

## 6. Wheel and Contact Geometry

The detailed specification does not provide tyre diameter, tyre width, or wheel-contact dimensions. However, the Rover has 250 mm of ground clearance and is designed to cross rocks, roots, kerbs, gravel, mud, and uneven outdoor terrain.

A preliminary wheel diameter of approximately 0.65 m is considered mechanically reasonable for the platform scale and stated ground clearance.

| Parameter | Preliminary Estimate |
|---|---:|
| Wheel diameter | 0.60–0.70 m |
| Nominal wheel diameter | 0.65 m |
| Nominal wheel radius | 0.325 m |
| Number of ground-contact regions | 4 |
| Support-polygon shape | Approximately rectangular |

The tyre width is not estimated at this stage because the specification does not provide a suitable visual or dimensional reference. Tyre width would strongly affect ground pressure, soft-terrain sinkage, and lateral traction and should therefore be obtained from a wheel specification or chassis drawing rather than inferred without sufficient evidence.

## 7. Intended Terrain Gradient

The detailed product specification defines the Rover’s incline capability directly.

| Operating Condition | Confirmed Gradient |
|---|---:|
| Sustained maximum incline | 30° |
| Momentary maximum incline | 35° |
| Energy-consumption reference gradient | 15° |

The intended sustained terrain gradient is therefore defined as:

**30° sustained grade**

The 35° value represents a momentary limit rather than a normal continuous operating condition. The specification also provides energy consumption at a 15° grade, indicating that 15° is a representative inclined operating case rather than only an extreme condition.

For mechanical scoping, the terrain-gradient categories are defined as follows:

| Terrain Case | Gradient | Interpretation |
|---|---:|---|
| Flat or low-gradient patrol | 0–5° | Normal roads, campuses, and paved infrastructure |
| Moderate outdoor incline | 5–15° | Access roads, solar farms, utility corridors |
| Demanding sustained incline | 15–30° | Maximum continuous multi-terrain operation |
| Momentary extreme incline | 30–35° | Short-duration traversal only |
| Above stated capability | Greater than 35° | Outside the confirmed operating envelope |

The incline capability assumes that sufficient wheel traction is available. Wet grass, mud, loose sand, gravel, and mixed surfaces may cause wheel slip before the geometric tipping boundary is reached. The Rover’s torque-vectoring and wheel-slip monitoring systems are therefore important parts of its terrain capability.

## 8. Preliminary Centre-of-Mass Height Estimate

The detailed specification does not provide the centre-of-mass location or the mass of individual structural subsystems. A preliminary centre-of-mass height is therefore estimated from the platform dimensions and component arrangement.

The Rover has an overall height of 1.71 m. Several heavy components are expected to be mounted relatively low:

- Four hub motors at wheel level.
- A welded aluminium structural frame.
- A 48 V, 200 Ah LiFePO4 battery pack.
- Suspension and wheel assemblies.
- Power electronics and motor controllers.

Higher-mounted components include:

- VLP-32 360-degree LiDAR.
- Forward solid-state LiDAR.
- PTZ camera.
- Thermal and multispectral cameras.
- Radar and acoustic sensors.
- Communication antennas.
- Sensor-support structures.

Because the battery, motors, and primary chassis structure are expected to account for a substantial proportion of the 395 kg unloaded mass, the centre of mass should be below the geometric mid-height of the 1.71 m platform.

The nominal centre-of-mass height is estimated as:

**Estimated centre-of-mass height: 0.70 m above ground**

A preliminary uncertainty range is:

**Estimated centre-of-mass height range: 0.60–0.85 m**

The lower end represents a configuration with batteries and major structural mass concentrated near the chassis floor. The upper end represents a configuration carrying a larger or heavier sensor package near the roof.

A preliminary mass-distribution assumption is shown below.

| Subsystem | Assumed Share of Unloaded Mass | Estimated Average Height |
|---|---:|---:|
| Wheels, hub motors, and suspension | 25% | 0.35 m |
| Battery and lower power hardware | 30% | 0.50 m |
| Chassis frame and body structure | 25% | 0.75 m |
| Computing and internal electronics | 10% | 0.95 m |
| Upper sensor package | 10% | 1.45 m |

This approximate distribution produces a centre-of-mass location close to the selected nominal value of 0.70 m.

The full-payload configuration may raise or shift the centre of mass depending on where the additional sensor payload is installed. Roof-mounted LiDAR, radar, cameras, communication hardware, or the optional solar panel would increase the centre-of-mass height. A manipulator or side-mounted payload could also move the centre of mass longitudinally or laterally away from the vehicle centreline.

## 9. Reference Coordinate System

A body-fixed coordinate system is defined for the platform description.

- The origin is located at the geometric centre of the rectangular wheel-contact area on the ground plane.
- The positive x-axis points forward along the 3.45 m vehicle length.
- The positive y-axis points towards the left side of the vehicle.
- The positive z-axis points vertically upwards.
- Wheelbase is measured parallel to the x-axis.
- Track width is measured parallel to the y-axis.
- Centre-of-mass height is measured parallel to the z-axis from the ground plane.
- The baseline centre of mass is assumed to lie on the longitudinal and lateral vehicle centreplanes.

The front-left, front-right, rear-left, and rear-right wheel contacts define an approximately rectangular support polygon.

## 10. Geometric Parameter Summary

| Parameter | Status | Selected Value |
|---|---|---:|
| Number of wheels | Confirmed | 4 |
| Overall length | Confirmed | 3.45 m |
| Overall width | Confirmed | 1.88 m |
| Overall height | Confirmed | 1.71 m |
| Unloaded mass | Confirmed | 395 kg |
| Maximum operational mass | Confirmed | 435 kg |
| Ground clearance | Confirmed | 0.25 m |
| Wheelbase | Estimated | 2.50 m |
| Track width | Estimated | 1.60 m |
| Wheel diameter | Estimated | 0.65 m |
| Nominal CoM height | Estimated | 0.70 m |
| CoM-height uncertainty range | Estimated | 0.60–0.85 m |
| Sustained incline | Confirmed | 30° |
| Momentary incline | Confirmed | 35° |
| Minimum turning radius | Confirmed | 0 m |
| Maximum speed | Confirmed | 1.5 m/s |

## 11. Explicit Geometric and Mechanical Assumptions

The following assumptions are adopted explicitly:

1. Aido Rover uses four ground-contact wheels.
2. Each wheel has a dedicated brushless electric hub motor.
3. Each wheel has independent suspension.
4. Steering is achieved through differential torque vectoring.
5. The vehicle can perform in-place rotation with a stated turning radius of 0 m.
6. The vehicle can perform lateral crab movement.
7. The chassis is represented as a rigid body for geometric scoping.
8. The four wheel-ground contact locations form an approximately rectangular support polygon.
9. The nominal wheelbase is estimated as 2.50 m.
10. The nominal track width is estimated as 1.60 m.
11. The nominal wheel diameter is estimated as 0.65 m.
12. The nominal centre-of-mass height is estimated as 0.70 m.
13. The unloaded centre of mass is assumed to lie on the longitudinal and lateral centreplanes.
14. The primary battery, drive motors, and structural mass are assumed to be mounted below the geometric mid-height.
15. The upper sensor package is assumed to contribute approximately 10% of unloaded vehicle mass.
16. The optional payload may change both the height and horizontal position of the centre of mass.
17. The full 150 kg payload capacity is not assumed to be included in the stated 435 kg maximum sensor configuration because the relationship between these two specification values requires clarification.
18. The platform operates on outdoor terrain including asphalt, gravel, grass, mud, loose sand, and rocky surfaces.
19. The stated 30° sustained incline assumes sufficient wheel-ground traction.
20. The stated 35° incline is treated as a momentary capability rather than a continuous operating condition.
21. Tyre deformation, suspension compression, and local terrain irregularities are excluded from the nominal geometry.
22. Body overhangs do not contribute directly to the wheel support polygon.
23. Wheelbase, track width, wheel diameter, and centre-of-mass height must be updated if a dimensioned chassis drawing becomes available.
24. The detailed March 2026 internal specification is treated as the controlling source where it conflicts with an earlier visual reference.

## 12. Important Specification Clarifications

The specification states that the unloaded platform mass is 395 kg and that the maximum mass with the full sensor payload is 435 kg, which implies a 40 kg installed sensor-package increase. It also states an additional sensor payload capacity of 150 kg.

These two values may describe different conditions:

- The 435 kg value may represent the standard full sensor configuration.
- The 150 kg value may represent the structural payload capacity available for optional equipment.
- The 150 kg capacity may not be intended to be added directly to the 435 kg operational configuration.

This distinction should be clarified before using a final maximum vehicle mass for detailed loading or stability work.

The specification also describes both mecanum/skid-steer in-place rotation and lateral crab movement. Conventional skid-steer wheels can rotate in place but do not normally provide true lateral crab movement. Lateral motion generally requires mecanum wheels, independently steerable wheel modules, or another omnidirectional mechanism. The exact wheel type and orientation should therefore be confirmed from a chassis image or drivetrain drawing.

## 13. Scoping Conclusion

Aido Rover is defined as a four-wheel, independently driven, independently suspended, multi-terrain autonomous platform. Each wheel uses a dedicated brushless hub motor, while differential torque vectoring provides terrain compensation and manoeuvring control.

The confirmed platform dimensions are 3.45 m in length, 1.88 m in width, and 1.71 m in height. The unloaded mass is 395 kg, increasing to 435 kg with the stated full sensor payload configuration. The platform has 250 mm of ground clearance, a stated zero-metre turning radius, a sustained incline capability of 30°, and a momentary incline capability of 35°.

For preliminary geometric definition, the wheelbase is estimated as 2.50 m, the track width as 1.60 m, the wheel diameter as 0.65 m, and the centre-of-mass height as 0.70 m above ground. These estimated values remain subject to confirmation from detailed CAD, a dimensioned chassis drawing, or physical measurements.
