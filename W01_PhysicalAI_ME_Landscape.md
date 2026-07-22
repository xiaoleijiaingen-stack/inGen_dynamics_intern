# Mechanical Engineering Briefs for InGen Physical AI Platforms

## Fari --- Mechanical Engineering Brief

Fari's primary mechanical engineering challenge is integrating its
computing hardware, sensing equipment, battery, mobility system, and
external enclosure into a compact companion robot while maintaining safe
temperatures and stable operation around elderly users. The most
relevant mechanical engineering discipline is **thermal engineering**,
supported by structures and product-safety considerations. Fari is
expected to operate for extended periods indoors, where its processor,
communication modules, sensors, motor drivers, and power electronics
continuously generate heat inside a relatively small enclosure. The key
operational loading condition is therefore sustained full-power
operation in a warm indoor environment with limited airflow,
particularly when the robot is stationary and natural convection is the
primary method of heat removal. In this condition, excessive internal
temperature could reduce electronics reliability, while an elevated
external surface temperature could create discomfort or risk for a
nearby user. A meaningful analysis for verifying Fari's mechanical
feasibility would be a **lumped thermal-resistance network analysis**
covering the complete heat path from the main electronics to the ambient
air. The analysis should estimate the steady-state electronics
temperature, compare alternative enclosure materials and surface areas,
and evaluate whether a passive heat spreader or external fins are
sufficient. This would provide an initial design requirement for
enclosure material, available cooling area, internal component
placement, and the possible need for active airflow before detailed CAD
or CFD work begins.

## Senpai --- Mechanical Engineering Brief

Senpai's primary mechanical engineering challenge is producing a
lightweight and expressive educational robot that can perform repeated
movements while remaining structurally stable, mechanically reliable,
and safe during interaction with children. The most relevant mechanical
engineering discipline is **mechanism design**, supported by lightweight
structures, fatigue analysis, and static stability. Since the robot is
intended for an educational environment, its mechanical system may
experience frequent actuation, repeated starts and stops, occasional
manual repositioning, and accidental contact from users. The key
operational loading condition is repeated upper-body or joint motion
combined with an external horizontal force applied near the top of the
robot. This condition may create high actuator torque, cyclic loading in
brackets and joints, bearing wear, fastener loosening, and an
overturning moment at the base. Because children may touch or push the
robot unexpectedly, the structure must tolerate these loads without
tipping, exposing pinch points, or allowing a mechanism to move with
excessive force. A meaningful analysis for verifying Senpai's mechanical
feasibility would be a **combined mechanism load and static-stability
analysis**. The study should estimate the maximum actuator and joint
loads during the most demanding motion, evaluate the restoring stability
provided by the base, and determine whether the centre of mass remains
safely within the support area during user contact. The results would
establish preliminary actuator capacity, joint and bracket requirements,
allowable upper-body mass, minimum base dimensions, and suitable safety
margins for repeated classroom operation.

## Sentinel Prime AI --- Mechanical Engineering Brief

Sentinel Prime AI's primary mechanical engineering challenge is
integrating multiple perception sensors and onboard computing equipment
into a compact patrol platform without obstructing sensor coverage,
losing alignment, or exposing the equipment to excessive vibration,
shock, and heat. The most relevant mechanical engineering discipline is
**structures**, with strong connections to sensor integration, vibration
control, thermal design, and mechanical packaging. A patrol system may
carry a 360-degree LiDAR, forward-facing depth or RGB cameras, thermal
sensors, communication hardware, and supporting electronics, all of
which must remain accurately positioned relative to one another. The key
operational loading condition is continuous patrol operation while the
sensor package is subjected to chassis vibration, motor excitation,
sudden terrain-induced shock, and elevated ambient temperature. These
loads may cause bracket deflection, fatigue, fastener loosening, cable
damage, sensor misalignment, or gradual calibration drift. A meaningful
analysis for verifying Sentinel Prime AI's mechanical feasibility would
be a **sensor-housing structural and field-of-view analysis**. The
analysis should verify that the LiDAR scan plane remains unobstructed,
the camera retains its required viewing angle, the mounting structure
can survive the selected shock condition, and the housing is
sufficiently stiff to avoid large vibration amplitudes near the motor
excitation range. It should also review cable-routing clearance and the
mechanical path available for heat transfer into the chassis. The
results would define the required mounting height, bracket stiffness,
attachment arrangement, sensor mass budget, and enclosure configuration
before development of a detailed SolidWorks assembly.

## Aido Rover --- Mechanical Engineering Brief

Aido Rover's primary mechanical engineering challenge is maintaining
manoeuvrability, structural integrity, traction, and resistance to
tipping while operating across irregular and sloped outdoor terrain. The
most relevant mechanical engineering discipline is **kinematics**,
supported by structures, rigid-body stability, and wheel--ground
interaction. Unlike a robot operating on a controlled indoor floor, Aido
Rover may encounter gradients, local terrain steps, loose surfaces,
uneven wheel contact, and restricted turning areas while carrying its
full equipment and sensor payload. The key operational loading condition
is maximum-mass operation on a slope or uneven terrain while the left
and right drive sides operate at different speeds during a turning
manoeuvre. This condition combines a changing turning centre, uneven
wheel reactions, lateral tyre slip, chassis loading, and an increased
risk of tipping if the centre of mass is too high or moves close to the
support boundary. A meaningful analysis for verifying Aido Rover's
mechanical feasibility would be a **planar drive-train kinematic and
anti-tipping analysis**. The analysis should define the assumed wheel
configuration, wheelbase, track width, wheel size, total mass, payload
position, and centre-of-mass height, then determine the expected turning
envelope and safe static terrain-gradient range. It should also examine
the sensitivity of stability to uncertain centre-of-mass height and
acknowledge that ideal skid-steer kinematics do not fully represent tyre
slip on real terrain. The results would provide clear deployment
constraints and establish the geometric and loading inputs required for
later chassis structural analysis and mechanism optimisation.
