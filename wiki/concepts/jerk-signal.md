---
type: concept
created: 2026-10-13
updated: 2026-10-15
sources: ["raw/s41467-025-66256-z.pdf", "raw/s41467-025-56689-x.pdf"]
tags: [jerk, early-warning, dyke, seismology, method]
---

# Jerk signal

A very-low-frequency transient in the **time derivative of horizontal ground acceleration** (units: nm·s⁻³). A single very-broadband seismometer records it while magma is fracturing its way out of a shallow reservoir. It is used as a real-time eruption alarm at [[piton-de-la-fournaise]]. Source: [[jerk-beauducel-2025]].

## Physical interpretation
- The source is **fracture opening** from a dyke or sill intrusion. At the station's distance of about 8 km, horizontal displacement dominates and tilt and vertical displacement are negligible. This follows from elastic half-space dislocation models (Okada), where they fall off as distance⁻², ⁻⁴ and ⁻³ respectively (p. 3, Fig. 3).
- In the [[horizontal-pendulum-seismometer]] equation, displacement enters as a second derivative and tilt does not. So the *acceleration* of opening controls the recorded signal. That makes Jerk an indicator of how fast fracturing is happening (p. 3).
- Earlier work had read these transients as tilt steps. But the tilt implied by the seismic signal was one to two orders of magnitude larger than what tiltmeters measured at the same site. This paper resolves that mismatch (p. 2).
- The particle motion is quasi-linear and points toward the source, which gives a rough location (p. 2, Fig. 1).

## Timing
It appears during the intense phase of the seismic swarm and fades when earthquakes slow down and the dyke propagates. The lead time before eruption ranges from a few minutes to 8.5 h, with a mean of about 2 h (pp. 3, 5).

## Detection pipeline (as deployed)
The input is [[mass-position-channel]] data (LMN/LME at 1 Hz) from [[rer-station]]. The pipeline has four steps (p. 6):
1. Remove tides.
2. Compute the derivative as a causal linear-trend slope (900 s window, 60 s step).
3. Convert to polar amplitude and azimuth.
4. Raise the alarm in two stages: 0.1 then 0.2 nm·s⁻³, with the azimuth within ±30° of N197.

It runs as a module in [[webobs]] at [[ovpf-ipgp]].

## Performance
92% of 24 eruptions over 2014–2023 in real time, with 14% false positives and AUC 0.85. Over 1998–2023, 42 of 48 eruptions had an alarm. Full breakdown and caveats: [[jerk-beauducel-2025]].

## Failure modes
- No fracturing means no Jerk. Examples are "silent" injection into rock that is already fractured (Dolomieu 2006, 2008) and short, fast summit dykes (2019-06-11, 2020-02-10).
- Noise from cyclones, ocean and station maintenance (p. 5).

## Transferability (authors' claim, untested)
The authors suggest it could work on other basaltic volcanoes with recurrent dyking that are poorly monitored, and name Reykjanes in Iceland as a candidate (p. 6). **Not demonstrated in the source.**

## Contrast: statistical transfer learning
[[ardid-dempsey-2025-transfer-learning]] forecasts eruptions the opposite way:
- **Model:** a random forest trained on 24 volcanoes, using 2–16 Hz vertical amplitude features ([[rsam-dsar]]) over 48 h windows.
- **Scope:** explosive (phreatic and magmatic) onsets only. Effusive eruptions are excluded.

Comparison table: [[transfer-learning-eruption-forecasting]]. The AUCs of the two methods (0.85 vs about 0.8) are not directly comparable. See [[forecast-evaluation-roc-auc]].

## Our use
Public post-2010 POS data is not openly available, so we plan to feed the method with LHE/LHN velocity converted to acceleration, the same workaround the paper used before 2010. See [[What LHE channel at RER Station is]].
