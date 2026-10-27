---
type: concept
created: 2026-10-13
updated: 2026-10-13
sources: ["raw/SEEDManual_V2.4_Appendix-A.pdf", "raw/s41467-025-66256-z.pdf"]
tags: [mass-position, channel, lm, seismometer]
---

# Mass-position (POS) channel

In [[seed-channel-naming]], instrument code **M** in slot 2 means *mass position*: where the seismometer's inertial mass sits. The manual gives units as "M/S\*\*2 (usually)" ([[seed-manual-appendix-a]], p. 124). Example: `LME` is the long-period (≈1 Hz), mass-position, east channel.

## As used for Jerk
- At [[rer-station]], LMN/LME are the real-time input to the [[jerk-signal]] detector ([[jerk-beauducel-2025]], p. 6).
- The POS frequency response is **flat**. The manufacturer does not supply a sensitivity, so the authors derived one by linear correlation with the LHN/LHE velocity channels after converting those to acceleration. Results: LMN 4.02613·10⁹ and LME 3.80261·10⁹ count/(m·s⁻²) (p. 6).
- RER had no POS signal before 2010, when new electronics were installed. Since then, POS data is only "available upon request" (pp. 6–7).

## Substitute
You can approximate the POS signal by converting the LH\* velocity channels to acceleration, but only in post-analysis because a detrend is needed. See [[What LHE channel at RER Station is]].
