---
type: concept
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-025-56689-x.pdf", "raw/s41467-020-17375-2.pdf"]
tags: [machine-learning, transfer-learning, forecasting, method, explosive]
---

# Transfer-learning eruption forecasting

Training an eruption forecaster on seismic data from **many volcanoes** and applying it to a volcano that has few or no recorded eruptions. Sources: [[ardid-dempsey-2025-transfer-learning]] (multi-volcano method) and [[dempsey-2020-whakaari-forecasting]] (its single-volcano predecessor). Page numbers without a year refer to the 2025 paper.

## Lineage: from one volcano to many
[[dempsey-2020-whakaari-forecasting]] built the pipeline for [[whakaari]] alone. It missed the 2016 eruption, whose precursor was unlike earlier ones, and concluded that data-driven models "only anticipate eruptions with precursors similar to those seen before". The paper proposed adding precursors from other volcanic systems as a remedy (2020, p. 4). [[ardid-dempsey-2025-transfer-learning]] carries this out across 24 volcanoes (2025, ref. 50 → 2020 paper).

| | Dempsey et al. 2020 | Ardid, Dempsey et al. 2025 |
|---|---|---|
| Training data | one volcano (Whakaari, station WIZ), 2011–2020 | 24 volcanoes, one station each, 41 eruptions |
| Streams | RSAM 2–5, MF 4.5–8, HF 8–16 Hz, modified DSAR (10 min); component not stated | same four streams (10 min), vertical component |
| Earthquake filtering | not described in the main text | regional and VT earthquakes removed (2 min envelope + 20 min moving minimum) |
| Transformations / normalization | 1/X, derivative and log₁₀ tested, "did not improve" (no normalization described in the main text) | log + z-score |
| Features | tsfresh, 759 (706 after dropping 53 correlated); 20 most significant per subset | tsfresh, more than 700 |
| Window / look-forward | 48 h / 48 h (both tested from 12 h to 5 days) | 48 h / 48 h |
| Model | 100 decision trees, each on a different undersampled set | random forest of up to 200 trees |
| Testing | leave one eruptive episode out (±1 month) | leave one volcano out (generalized); leave one eruption out (tailored) |
| Metrics | alert-based: MCC, eruption probability during an alert, alert duration | ROC / AUC |
| Code licence | MIT | CC BY-NC |

## Why
Most volcanoes have one or a few recorded eruptions, so a model trained on one volcano has almost nothing to learn from (p. 2). Older generalized methods have their own weaknesses (p. 2):
- *Analog* methods depend on expert judgment and aren't consistent from case to case.
- *Expert elicitation* is subjective.
- *Inter-eruption-interval* models fail on volcanoes with irregular activity.

The authors describe their approach as "a form of the analog method" in which an objective statistical selection replaces expert choice of analogs (p. 6).

## Scope: explosive eruptions
The method targets abrupt **phreatic and magmatic (explosive) onsets**. Effusive episodes are excluded (p. 8). Precursors that differ by eruption style don't transfer well. The Eyjafjallajökull 2010 fissure onset was signalled ambiguously, and the explosive phase that followed was signalled better (p. 5). → For effusive, dyke-fed basaltic systems such as [[piton-de-la-fournaise]], this method is **not validated**.

## How it works (as published)
1. **Data streams:** [[rsam-dsar]] (RSAM, MF, HF, DSAR) at 10-min resolution from one vertical-component station per volcano. Regional and VT earthquakes are filtered out, then values are log-transformed and z-scored (p. 8).
2. **Features:** more than 700 tsfresh statistics on 48 h windows, filtered by a Mann-Whitney U test with a Benjamini-Yekutieli false-discovery rate of 5% (p. 8).
3. **Labels:** a window is labelled 1 if its end falls within 48 h before an eruption onset. That gives about 164 positive windows against more than 50,000 negatives, so the negatives are randomly undersampled to balance the set, and the draw is repeated (p. 8).
4. **Model:** a random forest of up to 200 trees (scikit-learn). The output is the "consensus" (the mean of the trees' votes), between 0 and 1 (pp. 8–9).
5. **Pools:** separate models for magmatic, phreatic and world pools. Choosing the pool matters: sometimes the narrower pool beats the world pool (pp. 6, 9).
6. **Evaluation:** leave-one-volcano-out cross-validation for generalized models and leave-one-eruption-out for tailored ones, with forecasts made in 10-min steps, pseudo-prospectively. Scoring: [[forecast-evaluation-roc-auc]].

## Results in short
AUC is about 0.8 out-of-sample, which beats an RSAM baseline and is close to a tailored model (0.84 vs 0.87 mean). Skill levels off beyond about 8–12 volcanoes in the training pool ([[eruption-precursor-ergodicity]]).

## Limits
- False positives at some volcanoes (Ontake). Misses when the record before the eruption is short (Cordón Caulle) (p. 5).
- One station per volcano. Seismic data only.
- The model can't explain its output. The authors call real-time interpretability "outstanding".
- Mislabelled eruption dates "poison" training (pp. 4, 6).

## Contrast with Jerk
| | Transfer learning (this page) | [[jerk-signal]] |
|---|---|---|
| Basis | statistical, data-driven | physical (fracture opening) |
| Signal | vertical, 2–16 Hz amplitude/ratio | horizontal, very-low-frequency acceleration derivative |
| Volcanoes | 24, explosive onsets | 1, basaltic dyke intrusions |
| Horizon | 48 h likelihood | minutes to 8.5 h deterministic alarm |
| Output | consensus 0–1 | amplitude + azimuth threshold |

The two methods share no data and target different eruption styles. They are complementary ideas, not competitors on the same problem (our synthesis, not a claim from either paper).
