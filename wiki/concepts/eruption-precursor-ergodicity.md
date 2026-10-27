---
type: concept
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-025-56689-x.pdf", "raw/s41467-020-17375-2.pdf"]
tags: [ergodicity, forecasting, statistics, hypothesis]
---

# Ergodicity of eruption precursors

The hypothesis that the *ensemble* distribution of seismic signals across many volcanoes approximates the *temporal* distribution at a single volcano over a long time. If it holds, precursors learned at other volcanoes can forecast eruptions at a volcano that has little history of its own. Proposed in [[ardid-dempsey-2025-transfer-learning]].

## Evidence offered
- Out-of-sample AUC increases with the number of volcanoes in training, from about 0.35–0.65 with 1–2 volcanoes to about 0.8 with more than 8 (Fig. 3, p. 4). Without ergodicity, a larger ensemble would not be expected to help (p. 4).
- Specific features transfer. HF harmonics at 40 min and 3 h, learned from St. Helens 2004 and Semisopochnoi 2019, strengthen before Augustine 2006, which was not in training (Fig. 4).
- The authors cite analogous ergodic assumptions in seismic hazard (regional earthquake catalogs) and in regionalized flood forecasting (p. 6).

## Origin of the idea
[[dempsey-2020-whakaari-forecasting]] noted that a single-volcano model missed the 2016 [[whakaari]] eruption, whose precursor differed from earlier ones. It suggested adding "precursory signals from other volcanic systems", with the caution that this "would require testing and evaluation to ensure the unique signals identified for a particular volcanic system are not diluted" (2020, p. 4). In 2025 the generalized phreatic model strengthened its output before that same 2016 eruption (2025, p. 5, Fig. 5b). The 2025 paper also confirms the dilution risk: a larger pool can perform worse (2025, p. 6).

## Caveats (authors')
- It works "at a time series feature level". **No physical mechanism is proposed** for the shared features (Fig. 4 caption).
- Spurious correlations can't be excluded (Fig. 4 caption).
- "Ergodicity is not a bottomless well". Skill levels off at AUC ≈ 0.8, and mixing eruption styles can add noise (p. 6).
- Shown only for explosive (phreatic and magmatic) onsets. See [[transfer-learning-eruption-forecasting]].

## Relevance to volcan-eye
The [[jerk-signal]] rests on the opposite premise: a specific physical process at one well-instrumented volcano. Whether an ergodic, multi-volcano approach could also work for effusive dyke intrusions at [[piton-de-la-fournaise]] is **open**. Neither source tests it.
