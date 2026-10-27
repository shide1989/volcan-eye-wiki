---
type: overview
created: 2026-10-13
updated: 2026-10-19
sources: ["raw/SEEDManual_V2.4_Appendix-A.pdf", "raw/s41467-025-66256-z.pdf", "raw/s41467-025-56689-x.pdf", "raw/s41467-020-17375-2.pdf", "raw/Data_access_at_IPGP-DC.pdf"]
tags: [overview]
---

# Overview

**Status: early.** Five sources ingested.

## Current thread
The working question is which open seismic data from [[geoscope]] station [[rer-station]] (La Réunion) can feed a detector based on the [[jerk-signal]].

**The method** ([[jerk-beauducel-2025]]): Jerk is the time derivative of horizontal acceleration recorded by a single very-broadband seismometer 8 km from the summit of [[piton-de-la-fournaise]]. The authors interpret it as fracture opening during dyke injection, not as tilt (see [[horizontal-pendulum-seismometer]]). Running in real time at [[ovpf-ipgp]] in [[webobs]], it alerted before 92% of 24 eruptions in 2014–2023, with 14% false positives and lead times from minutes to 8.5 h.

**The data problem:** the real-time input is the [[mass-position-channel]] pair LME/LMN. After 2010 that data is only available on request. [[What LHE channel at RER Station is]] concludes that the open LHE/LHN velocity channels, converted to acceleration, can stand in for it. The paper itself did exactly this for eruptions before 2010, which confirms the approach is workable. **Open issue:** the paper says the conversion is only reliable in post-analysis because of the detrend, so a real-time LHE-based version still needs to be designed. Channel codes are decoded in [[seed-channel-naming]] ([[seed-manual-appendix-a]], [[fdsn]]).

**Access path:** the open data for network G (RER) and the PF network is archived by the [[ipgp-data-center]] and served through [[fdsn-web-services]] at `https://ws.ipgp.fr`, also reachable with ObsPy `Client('IPGP')` ([[ipgp-dc-data-access]]). Querying RER this way is deferred.

## Context: the other school of forecasting
[[ardid-dempsey-2025-transfer-learning]] shows a statistical alternative to Jerk:
- **Model:** a random forest trained on seismic amplitude features ([[rsam-dsar]]) from 24 volcanoes and tested on volcanoes it never saw ([[transfer-learning-eruption-forecasting]]).
- **Result:** out-of-sample AUC ≈ 0.8, explained by the "ergodicity" of precursors ([[eruption-precursor-ergodicity]]).
- **Scope:** the approach **mainly concerns explosive volcanoes**. Effusive eruptions were excluded, and Piton de la Fournaise is not in the dataset.

Its predecessor, [[dempsey-2020-whakaari-forecasting]], applies the same pipeline to [[whakaari]] alone, using one station from 2011 to 2020:
- **Hits:** at an alert threshold of 0.8 it warned before 5 of 7 eruptions, including 17 h before the fatal 2019 eruption.
- **Cost:** alerts covered 8.5% of the time, and an eruption occurred during only 8.6% of them.
- **Miss:** the 2016 eruption, which the authors interpret as purely hydrothermal. That miss motivated the move to multiple volcanoes.

So it is background, not a ready tool for our effusive, dyke-fed target. It also needs higher-rate channels than RER's 1 Hz LH\*. The AUCs of the two methods are not comparable ([[forecast-evaluation-roc-auc]]).

## Open flags
- ✅ Resolved 2026-10-19: the two Réunion DOIs are different but linked. 10.18715/REUNION.OVPF is the OVPF data collection, and it contains 10.18715/reunion.PF, the PF network dataset (DataCite). See [[ovpf-ipgp]].
- Two internal inconsistencies in the Jerk paper: a 2012 vs 2014 start date, and 24 vs 21 eruptions in the post-processing set. See [[jerk-beauducel-2025]].
- The supplementary tables (eruption list, alarm times) are not in `raw/`. They would settle the second inconsistency.
- Three inconsistencies in the Ardid/Dempsey paper: 15 vs 16 magmatic eruptions, AUCs that differ between Fig. 2 and Table 1, and Holuhraun (largely effusive) on the map despite the stated exclusion of effusive eruptions. See [[ardid-dempsey-2025-transfer-learning]].
- Dempsey 2020 dates the fatal Whakaari eruption both 9 and 12 December 2019. The paper's own figures support 9 December. See [[dempsey-2020-whakaari-forecasting]].

## Not yet ingested (in `raw/`)
- `raw/BOUE_2015_archivage.pdf`
