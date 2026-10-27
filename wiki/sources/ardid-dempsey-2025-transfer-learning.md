---
type: source
created: 2026-10-15
updated: 2026-10-19
sources: ["raw/s41467-025-56689-x.pdf"]
tags: [machine-learning, transfer-learning, forecasting, rsam, dsar, explosive, phreatic, magmatic]
---

# Ergodic seismic precursors and transfer learning for short term eruption forecasting at data scarce volcanoes (Ardid, Dempsey et al. 2025)

**Origin:** Ardid A., Dempsey D. (equal contribution), Caudron C., Cronin S., Kennedy B., Girona T., Roman D., Miller C., Potter S., Lamb O.D., Martanto A., Cubuk-Sabuncu Y., Cabrera L., Ruiz S., Contreras R., Pacheco J., Mora M.M., De Angelis S. (2025). *Nature Communications* 16:1758. https://doi.org/10.1038/s41467-025-56689-x. Received 2024-02-15, published 2025-02-25. Open access (CC BY 4.0).

## What it is
A **statistical / machine-learning** approach to short-term (48 h) eruption forecasting at volcanoes with few or no recorded eruptions. A random-forest model is trained on seismic precursors from a *pool* of volcanoes and tested on a volcano it has never seen. Its counterpart in this wiki is the physics-based, single-volcano [[jerk-signal]] ([[jerk-beauducel-2025]]). See [[transfer-learning-eruption-forecasting]].

**Predecessor:** [[dempsey-2020-whakaari-forecasting]] (ref. 50), the single-volcano Whakaari pipeline this paper generalizes.

## ⚠️ Scope: explosive onsets only
The model targets "the initial abrupt, impulsive (phreatic and magmatic) onset of eruption". The authors **excluded effusive eruptive episodes**, along with geysering and passive ash emission. They name effusive eruptions as future work (p. 8). So the method **mainly concerns explosive volcanoes** (user steer, 2026-10-15). It says nothing directly about the effusive basaltic eruptions of [[piton-de-la-fournaise]], which is not in the dataset.

## Key takeaways
1. **Dataset.** 41 eruptions at 24 volcanoes, about 73 years of seismic record in total, with **one station per volcano** (the one with the most eruptions and closest to the vent) (pp. 1, 7). Of the 24 volcanoes, only 3 have more than 3 eruptions and 11 have a single recorded eruption (p. 2).
2. **Three volcano pools** (p. 9, Fig. 1b):
   - *Magmatic:* Redoubt, Augustine, Veniaminof, Pavlof, Great Sitkin, Semisopochnoi, Okmok, Bezymianny, St. Helens.
   - *Phreatic:* Whakaari, Ruapehu, Tongariro, Ontake, Copahue, Kawah Ijen. All have well-developed hydrothermal systems.
   - *World:* all volcanoes.
3. **Out-of-sample skill** (leave-one-volcano-out, pseudo-prospective). AUC is about 0.80 for all three pools. The RSAM baseline scores 0.50 (magmatic), 0.74 (phreatic) and 0.58 (world). Generalized models nearly match tailored models trained on the target volcano itself: mean AUC 0.84 vs 0.87 (Table 1, Fig. 2). Scoring method: [[forecast-evaluation-roc-auc]].
4. **Ergodicity.** Skill rises with the number of volcanoes in the training pool and levels off at AUC ≈ 0.8 above about 8–12 volcanoes (Fig. 3). The authors read this as evidence that eruption precursors are *ergodic*: a group of volcanoes can stand in for one volcano's long history. They do **not** propose a physical mechanism, and say spurious correlations can't be excluded (Fig. 4 caption). See [[eruption-precursor-ergodicity]].
5. **Pipeline.**
   - Input: vertical velocity, cut into 10-min samples and split into four streams. RSAM is 2–5 Hz, MF is 4.5–8 Hz, HF is 8–16 Hz, and DSAR is the MF/HF ratio (see [[rsam-dsar]]).
   - Earthquake removal: regional and volcano-tectonic (VT) earthquakes are filtered out first (p. 8).
   - Normalization: values are log-transformed and z-scored.
   - Features: 48 h windows with more than 700 *tsfresh* features. They are kept only if they pass a Mann-Whitney U test with a Benjamini-Yekutieli false-discovery rate of 5%.
   - Model and output: random forests of up to 200 trees, trained on a balanced set where the label is 1 if an eruption starts within 48 h. The output is a "consensus" score between 0 and 1 (p. 8).
6. **Failure modes** (pp. 5, 7, Fig. 5):
   - Cordón Caulle 2011 was missed. Its record began only 20 days before the eruption, the station is 10 km from the crater, and the eruption was weakly signalled geodetically.
   - Ontake 2014 had a high false-positive rate.
   - At Copahue, the output stayed high between closely spaced eruptions.
   - At Eyjafjallajökull 2010, the fissure phase was signalled ambiguously. The forecast was better for the explosive phase that followed. The authors suggest the closed-conduit fissure onset behaves differently from the explosive phase.
   - The method gives a likelihood, **not the size** of the eruption.

## Notable cases
- **Improved over tailored models:** Bezymianny 2009 and [[whakaari]] 2016. The paper says the 2016 Whakaari eruption had been hard to anticipate in earlier studies, citing ref. 28, Dempsey et al. 2022, which is not in `raw/`. This is consistent with [[dempsey-2020-whakaari-forecasting]], which missed it entirely (p. 5, Fig. 5a–b).
- **Precursor transfer illustrated:** HF harmonics at 40 min and 3 h, selected from St. Helens 2004 and Semisopochnoi 2019, appear again before Augustine 2006, which was not in training (Fig. 4).

## Code and data
- Library *Puia* (Supplementary Code 1), licence **CC BY-NC**: commercial use needs permission (p. 10).
- Pre-processed 10-min amplitude data is in Supplementary Data 1. Raw waveforms come from GeoNet (New Zealand) and IRIS (Alaska), served through FDSN web services (p. 10; cf. [[fdsn]]).

## Flags (not resolved)
- ⚠️ **Number of magmatic eruptions.** The text says the magmatic model involves "9 volcanoes and **16** eruptions" (p. 2). The Fig. 1c caption and panel say "Magmatic pool, **15** eruptions" (p. 3).
- ⚠️ **Fig. 2 vs Table 1 AUCs.** For Bezymianny, the generalized model is 0.72 in Fig. 2d but 0.75 in Table 1. For Copahue, the tailored model is 0.94 in Fig. 2f but 0.96 in Table 1 (pp. 4–5).
- ⚠️ **Volcano count and effusive exclusion.** The Fig. 1a map labels 23 volcanoes, not 24. It also includes **Holuhraun** (Iceland, 2014). The Holuhraun eruption is usually described as a largely effusive fissure eruption, but that description is general knowledge, not from this source. This sits awkwardly with the stated exclusion of effusive episodes. How Holuhraun was labelled is presumably in Supplementary Table S2, which is not in `raw/`.

## Used by
[[dempsey-2020-whakaari-forecasting]], [[whakaari]], [[transfer-learning-eruption-forecasting]], [[eruption-precursor-ergodicity]], [[rsam-dsar]], [[forecast-evaluation-roc-auc]], [[jerk-signal]], [[piton-de-la-fournaise]], [[overview]].
