---
type: concept
created: 2026-10-13
updated: 2026-10-13
sources: ["raw/s41467-025-66256-z.pdf"]
tags: [seismometer, tilt, physics, instrument]
---

# Horizontal pendulum seismometer (acceleration vs tilt)

A horizontal seismometer cannot tell ground acceleration apart from tilt. The paper gives the recorded horizontal acceleration as (Eq. 1, p. 2):

a_rad(t) = −ü_rad(t) − g·τ_rad(t) − d·Ω̇_z(t)

- ü_rad is the radial horizontal translation acceleration.
- τ_rad is the tilt about the tangential axis, multiplied by gravity g.
- Ω_z is rotation about the vertical axis and d is the distance of the mass. This rotation term is weak and usually neglected.

## Consequences
- At short periods (<100 s) the response is dominated by displacement. At long periods (>360 s) tilt becomes a significant part of the signal (p. 2).
- Without independent data you cannot separate the terms. However, a *continuous* (step) component can only come from tilt, because displacement enters as a second derivative (pp. 2–3).
- This is why the [[jerk-signal]] can be read as fracture-opening acceleration and not as tilt.
- The ratio η of horizontal displacement to tilt (m·rad⁻¹) is fixed for a given source and station. For a 100×100 m, 1 m opening about 7 km away, η ≈ −5×10⁵ for a vertical dyke and ≈ −2×10⁴ for a sill (p. 7, synthetic Jerk).

Source: [[jerk-beauducel-2025]]. Instrument example: the STS-1 sensors at [[rer-station]].
