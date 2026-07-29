# Week 2 Mechanical Engineering Log

## What was modelled

This week I built a planar drive-train model for Aido Rover using the confirmed four-wheel independent-drive architecture and the preliminary geometry defined during Week 1. The model used a 2.50 m wheelbase, 1.60 m track width, 0.70 m centre-of-mass height and the maximum stated 435 kg sensor configuration. I evaluated the ideal instantaneous centre of rotation and turning radius as the left/right wheel-speed ratio changed, then calculated longitudinal and lateral static tipping limits, slope-dependent wheel reactions and ground-pressure sensitivity.

## What the results revealed

Counter-rotating the left and right wheel sets gives a zero centre-path turning radius, which is consistent with the product specification. However, the body still sweeps a 3.93 m diameter during a complete in-place rotation. The theoretical static tipping limits are 60.8 degrees longitudinally and 48.8 degrees laterally, so lateral stability governs. Both values exceed the stated 30-degree sustained grade. This suggests that traction, wheel slip, suspension articulation and terrain irregularity are more likely to limit deployment than rigid-body static tipping. At a 30-degree lateral slope, each uphill wheel carries only about 457 N, compared with 1,391 N on each downhill wheel.

## Next question

The largest uncertainty is the tyre-ground contact model. Tyre width, pressure, stiffness and measured contact area are unavailable, so the nominal 28.4 kPa ground-pressure result is only a first estimate. The next question is what tyre and suspension data are required to determine whether the 30-degree grade is traction-limited or stability-limited on wet grass, mud and loose gravel.
