---
type: source
created: 2026-10-13
updated: 2026-10-13
sources: ["raw/s41467-025-66256-z.pdf"]
tags: [jerk, early-warning, piton-de-la-fournaise, rer, broadband, mass-position, dyke]
---

# Jerk, a promising tool for early warning of volcanic eruptions (Beauducel et al. 2025)

**Origin:** Beauducel F., Roult G., Ferrazzini V., Peltier A., Jousset P., Boissier P., Villeneuve N. (2025). *Nature Communications* 16:11418. https://doi.org/10.1038/s41467-025-66256-z. Received 2025-04-24, published 2025-12-17. Open access (CC BY-NC-ND 4.0).

## What it is
The paper introduces the [[jerk-signal]]: an automated, deterministic eruption early-warning method that uses **one** very-broadband seismometer, [[rer-station]], 8 km from the summit of [[piton-de-la-fournaise]]. The authors contrast it with the probabilistic, multi-parameter forecasting that observatories usually rely on (p. 1). It has run in real time at [[ovpf-ipgp]] inside [[webobs]] since 2014.

## Key takeaways
1. **The signal.** Jerk is a very-low-frequency transient in horizontal ground acceleration. The name refers to the time derivative of acceleration. It appears during the most intense part of the pre-eruptive seismic swarm (p. 2). The authors model it as caused by **horizontal displacement from fracture opening** (dyke/sill dislocation), not by tilt. At about 8 km, tilt and vertical displacement fall off with distance⁻⁴ and ⁻³, and horizontal displacement with ⁻². So the horizontal displacement term dominates at the station (p. 3, Fig. 3). Physics: [[horizontal-pendulum-seismometer]].
2. **Real-time record, 2014–2023.** There were 22 successful alarms before 24 eruptions (92%). There were 2 false negatives (late alarms on 2019-06-11 and 2020-02-10, both summit eruptions), 2 false positives (intrusions with no eruption, 2020-09-28 and 2021-10-10) and 12 true negatives. That gives a 14% false-positive rate. ROC AUC is 0.85, and 0.1 nm·s⁻³ is the optimal threshold. Lead time ranged from a few minutes to 8.5 h. The first automatic alarm came on 2014-06-20 at 20:33 UT, 1 h before tremor. The last recorded Jerk was on 2023-07-02, 40 min before eruption, with an amplitude of 1.5 nm·s⁻³ (pp. 1–2, Figs. 1–2).
3. **Algorithm.** The inputs are the **LMN/LME** mass-position channels at 1 Hz (see [[mass-position-channel]]). Processing steps:
   - Remove Earth and ocean tides (Gotic2 / NAO.99L, with amplitude factor and time shift fitted by Nelder–Mead on the 12 h residual).
   - Compute the derivative as a causal linear-trend slope over a 900 s window, resampled every 60 s, on a 5-day moving window.
   - Convert to polar amplitude and azimuth.
   - Alarm level 1 is 0.1 nm·s⁻³ and level 2 is 0.2 nm·s⁻³. The azimuth must also be within ±30° of N197, the direction of the summit.
   - Each level change sends an email.
   Background noise is usually below 0.05 nm·s⁻³. Processing adds 10–15 min of delay (pp. 3, 6).
4. **Retrospective analysis.** Re-processing 1998–2010 data shows a timely alarm would have been sent for 83% of eruptions. The misses were September 1999 (electronics before 2001), and August 2006 and December 2008 (inside the Dolomieu crater, through already-fractured rock). Over 1998–2023, 42 of 48 eruptions were preceded by an alarm, with a mean lead time of about 2 h (pp. 3, 5, Fig. 4).
5. **Limits and false-alarm sources.** False alarms come from technical work on the station (acceleration far above the maximum observed Jerk of 2.8 nm·s⁻³), from cyclones (Fakir, 2018-04-24: the motion is not linear and not toward the summit) and from oceanic noise. The method also needs fracturing to happen: a "silent" injection through rock that is already fractured gives no Jerk. Humans still validate alarms during maintenance and storms. Every Jerk alarm so far has been followed by magma injection (pp. 5–6).

## Data and calibration details (relevant to our RER thread)
- RER sensors: two Streckeisen **STS-1H** horizontal sensors and one **STS-1V** vertical sensor, with a 360 s period. Since 2010 the station has had **Metrozet STS1-E300** electronics and a 26-bit **Quanterra Q330HR** digitizer. It sits in a 4 km EDF tunnel, and the temperature varies by less than 0.5 °C per year (p. 6).
- The POS channels have a flat frequency response. Their sensitivity was obtained by linear correlation with **LHN/LHE** after removing the instrument response and converting to acceleration (SAC). Results: 4.02613·10⁹ count/(m·s⁻²) for LMN and 3.80261·10⁹ for LME (p. 6).
- **Before 2010 the station had no POS signal.** The authors converted the LHE/LHN velocity signals to acceleration and applied the same processing. That conversion only works in post-analysis, because removing the response needs a preliminary detrend (p. 6).
- Data: RER raw data is at http://geoscope.ipgp.fr. **POS (LM\*) data after 2010 is "available upon request"**. Processed data is at https://doi.org/10.18715/IPGP.2025.mebk5l9d (p. 7).
- Code: WebObs with the Jerk module, https://ipgp.github.io/webobs. Gotic2 is also available (p. 7).

## Contradictions inside the paper (flagged, not resolved)
- ⚠️ **Start date.** Results says the system was "developed and implemented" in **April 2014** (p. 2). Discussion says "**Since 2012** the real-time Jerk alarm has become a very efficient early warning tool" (p. 5).
- ⚠️ **Size of the post-processing set.** The text says **24 eruptions, 1998–2010**, with 83% alerted (p. 3). The Fig. 4 caption says **21 eruptions, 1998–2013** (p. 6). The 21 may count only eruptions that had an alarm, but 21/24 = 87.5%, not 83%. The supplementary tables (not in `raw/`) should settle it.

## Used by
- [[What LHE channel at RER Station is]]: confirms the claims about LHE/LME use and data availability.
- [[forecast-evaluation-roc-auc]]: its AUC 0.85 compared with [[ardid-dempsey-2025-transfer-learning]], with caveats.
- [[jerk-signal]], [[horizontal-pendulum-seismometer]], [[mass-position-channel]], [[rer-station]], [[piton-de-la-fournaise]], [[geoscope]], [[ovpf-ipgp]], [[webobs]].
