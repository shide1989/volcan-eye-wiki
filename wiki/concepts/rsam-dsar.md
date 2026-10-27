---
type: concept
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-025-56689-x.pdf", "raw/s41467-020-17375-2.pdf"]
tags: [rsam, dsar, seismic-amplitude, tremor, data-stream]
---

# RSAM, MF, HF and DSAR

Continuous seismic amplitude measures used for volcano monitoring and as machine-learning inputs. Definitions follow [[ardid-dempsey-2025-transfer-learning]] (p. 8) and, identically for the bands, [[dempsey-2020-whakaari-forecasting]] (p. 5). All are computed from velocity with the instrument response removed, in non-overlapping **10-min** windows (mean absolute velocity). The 2025 paper specifies the **vertical** component; the 2020 main text says only "raw seismic velocity data" and does not name a component.

| Stream | Band | Intent |
|---|---|---|
| **RSAM** (Real-time Seismic Amplitude Measurement) | 2–5 Hz | volcanic tremor; excludes ocean microseism (< 1 Hz) |
| **MF** (medium frequency) | 4.5–8 Hz | attenuation-sensitive band |
| **HF** (high frequency) | 8–16 Hz | attenuation-sensitive band |
| **DSAR** (Displacement Seismic Amplitude Ratio) | ratio of the integrated MF and HF signals. Dempsey 2020's "modified DSAR": u_DSAR = u_MF / u_HF, where u_k is the 10-min mean absolute value of ∫v_k dt | high values linked to gas accumulation or reduced fluid motion in the edifice (2025, p. 8) |

- Elsewhere, RSAM is sometimes computed unfiltered or over a broad band (0.5–20 Hz). Both papers use 2–5 Hz (2025, p. 8; 2020, p. 5).
- RSAM is widely used at observatories. In Ardid 2025, a simple RSAM percentile forecast (6 h rolling median) is used as the **benchmark**. It scored AUC 0.50, 0.74 and 0.58 on the magmatic, phreatic and world pools, well below the ML models. Its best results were on phreatic volcanoes (2025, p. 2, Table 1). The authors say this "is not intended to denigrate the value of RSAM", only that ML extracts more from it (2025, p. 3).

## Features found informative at Whakaari
From [[dempsey-2020-whakaari-forecasting]], p. 2 and Fig. 1d–g:
- The RSAM Fourier coefficient at **40-min** periodicity, RSAM **maximum**, and RSAM **4-h** periodicity were significant precursors.
- The gradient of **1/RSAM**, which failure-forecast modelling uses to extrapolate eruption onset, was "less remarkable" on its own.
- Transforming the streams (1/X, derivative, log₁₀) "did not improve forecasting ability" (2020, p. 5).

Seismic tremor is described there as "a continuous, long-period seismic signal in the 1–15 Hz frequency band" (2020, p. 2).

## Note for the RER thread (our inference, not from the source)
These bands need sampling rates of at least about 32 Hz (HF goes up to 16 Hz). [[rer-station]]'s **LH\*** channels are 1 Hz (Nyquist 0.5 Hz, see [[seed-channel-naming]]), so they **cannot** produce RSAM, MF, HF or DSAR as defined here. A higher-rate channel (B\*/H\*) would be needed. The [[jerk-signal]] instead uses the very-low-frequency band that LH/LM channels do cover.
