---
type: source
created: 2026-10-13
updated: 2026-10-13
sources: ["raw/SEEDManual_V2.4_Appendix-A.pdf"]
tags: [seed, fdsn, channel-naming, metadata, standard]
---

# SEED Manual v2.4, Appendix A: Channel Naming

**Origin:** *Standard for the Exchange of Earthquake Data, Reference Manual*, SEED v2.4, Appendix A (pp. 123–130), contributed by Scott Halbert. Published by the [[fdsn]]. Online copy: http://www.fdsn.org/pdf/SEEDManual_V2.4_Appendix-A.pdf

## What it is
This appendix defines the recommended way to name channels with three letters: **band + instrument + orientation**. The FDSN recommends it to member networks as a usage standard. SEED itself does not require it. The goal is to let data from cooperating networks be combined and to let like channels be found automatically. Full breakdown: [[seed-channel-naming]].

## Key takeaways
1. **Three letters, three aspects.** Letter 1 is the band (sample rate and response band). Letter 2 is the instrument family, i.e. what is measured. Letter 3 is the orientation (direction, or sometimes an instrument-specific meaning). (p. 123–124)
2. **Band is set by sample rate. For fast bands, corner period also counts.** Pairs split at a 10 s corner period: H/E (80–250 Hz), B/S (10–80 Hz), C/D (250–1000 Hz), F/G (1000–5000 Hz). Slower bands go by rate alone: M (>1 to <10 Hz), L (≈1 Hz), V (≈0.1 Hz), U (≈0.01 Hz), then R/P/T/Q for periods of hours to days. The manual says: "The sample rate should be used for the correct Band Code." (p. 124)
3. **A letter's meaning depends on its position.** `H` as a band is High Broad Band. `H` as an instrument is High Gain Seismometer. Seismometer instrument codes are H high gain, L low gain, G gravimeter, M mass position, N accelerometer (FDSN convention since Aug 2000). (p. 124)
4. **Orientation rule.** Use N/E only if the sensor is within 5° of north/east. Otherwise use 1/2/3. Record the true dip and azimuth in blockette 52. (p. 124)
5. **Typical GSN sets.** EH\* short period 100 sps, BH\* broadband 20 sps, LH\* long period 1 sps, VH\* very long period 0.1 sps. Special channels include LOG (console log, sample rate 0), SOH, ACE (clock error), LCQ (1 Hz clock quality), OCF (configuration file). (p. 130)

## Other details worth keeping
- Seismometer signal units: M, M/S, M/S\*\*2. For G and M channels the unit is "M/S\*\*2 (usually)". (p. 124)
- `X` (derived/synthetic) and `Y` (non-specific instrument) channels must carry a Channel Comment Blockette (059) with a URL that documents provenance, plus a short description in field 7 of B052. (p. 129)
- Instrument codes relevant to volcano monitoring: A tiltmeter (radians), D pressure/infrasound/hydrophone (Pa), F magnetometer (T), K temperature, S linear strain, V volumetric strain, Q electric potential, J rotational sensor. (pp. 125–128)

## Used by
- [[What LHE channel at RER Station is]]: decoding RER's `LHE` and `LME` channels.
