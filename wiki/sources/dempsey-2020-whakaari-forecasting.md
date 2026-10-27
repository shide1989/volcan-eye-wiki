---
type: source
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-020-17375-2.pdf"]
tags: [machine-learning, forecasting, whakaari, phreatic, explosive, rsam, dsar, decision-tree]
---

# Automatic precursor recognition and real-time forecasting of sudden explosive volcanic eruptions at Whakaari, New Zealand (Dempsey et al. 2020)

**Origin:** Dempsey D.E., Cronin S.J., Mei S., Kempa-Liehr A.W. (2020). *Nature Communications* 11:3562. https://doi.org/10.1038/s41467-020-17375-2. Received 2020-04-06, accepted 2020-06-29, published 2020-07-16. Open access (CC BY 4.0).

## What it is
A machine-learning eruption forecaster for **one volcano**, [[whakaari]], using **one seismic station**. It is the single-volcano ("tailored") predecessor of the multi-volcano method in [[ardid-dempsey-2025-transfer-learning]], which cites it as ref. 50 for the pipeline. Lineage and comparison: [[transfer-learning-eruption-forecasting]].

## Scope: explosive and phreatic onsets only
The target is "hazardous impulsive/explosive eruptions with the highest threat to visitors". The following were excluded: lava dome growth (Sep–Nov 2012), intermittent mud and ash eruptions (Jan–Apr 2013), a minor ash emission (Sep 2016), geysering and passive ash emission (pp. 2, 5). Like the 2025 paper, it says nothing about effusive basaltic systems such as [[piton-de-la-fournaise]].

## Data
- **Station:** WIZ, a GeoNet broadband station about 1 km southeast of the main vents. The second island station, WSRZ, did not cover all eruptions and was not used (pp. 2, 5).
- **Period:** 2011-01-01 to 2020-01-01, 9 years. About 85 days are missing (2.5%) and were filled by linear interpolation. All gaps fall in non-eruptive periods (p. 5).
- **Streams:** velocity with the instrument response removed, band-pass filtered into RSAM (2–5 Hz), MF (4.5–8 Hz) and HF (8–16 Hz). Each band's mean absolute amplitude is taken over non-overlapping 10-min windows. A fourth stream is a "modified DSAR": the MF and HF signals are integrated, their 10-min mean absolute values computed, and the ratio u_MF/u_HF taken (p. 5). See [[rsam-dsar]].
- **Transformations tested:** inverse (1/X), derivative and log₁₀. They "did not improve forecasting ability" (p. 5).
- **Eruptions** (Methods wording, all times UTC; p. 5). Five episodes containing seven eruptions:

| # | Date / time (UTC) | Description |
|---|---|---|
| 1 | 2012-08-04 16:52 | phreatic eruption, ash and blocks |
| 2 | 2013-08-19 22:23 | minor steam eruption ("steam and mud" in Results, p. 2) |
| 3 | 2013-10-03 12:35; 2013-10-08 02:05; 2013-10-11 07:09 | minor phreatic; steam and mud; moderate explosive. Treated as one episode |
| 4 | 2016-04-27 09:37 | moderate phreatic, six events within 35 min |
| 5 | 2019-12-09 01:11 | fatal eruption: 21 of 47 tourists and guides killed or fatally injured (p. 2). ⚠️ The date is inconsistent in the paper, see Flags |

## Method
- **Windows:** 48 h long with 36 h overlap (η = 0.75). Each window is timestamped at its last sample, which keeps future labels separate from past features and guards against data leakage (pp. 2, 5).
- **Labels:** 1 if an eruption occurs in the 48 h look-forward after the window, else 0 (p. 2).
- **Features:** tsfresh computes **759** features per window and stream, covering distribution, autocorrelation (FFT, PSD), linear-regressor terms, energy, entropy and so on. FFT periods for a 48 h window of 10-min samples run from 8.3·10⁻⁴ to 5.8·10⁻⁶ Hz (p. 5). Then **53** highly correlated linear-trend features were dropped (p. 6). Results reports **706** features (p. 2). 759 − 53 = 706, so that is the likely reconciliation (our arithmetic, not stated by the authors).
- **Feature selection:** a Mann-Whitney U test ranks features by p-value. A Benjamini-Yekutieli correction checks for false discovery: 99.3% of features are below a false-discovery threshold of 5%. The p-values of the selected features range from 10⁻¹⁰ to 10⁻² (pp. 2, 6).
- **Balancing:** a typical training set has 6,453 windows, of which 16 are labelled 1. Each training subset keeps those 16 plus 21 randomly drawn label-0 windows (0.3%), so N_ru = 37 and the undersampling ratio is 0.75. This is repeated N_cl = 100 times. Overall about 30% of non-eruptive data is used, and 69% of non-eruptive windows are never used to train any tree (p. 6).
- **Classifier:** each subset uses its 20 most significant features. Seven scikit-learn classifiers were compared: decision tree, k-nearest neighbours, SVM, logistic regression, random forest, naive Bayes and neural network. The **decision tree** consistently did best on model confidence while keeping alert duration low, so only decision-tree results are reported. The 100 trees together form "a random forest specialized on eruptive windows" (pp. 3, 6).
- **Output:** the ensemble mean ŷ, from 0 to 1, updated **every 10 min**. The authors state that it **cannot be interpreted as a probability** because the models are not calibrated (p. 6).
- **Alerts:**
  - An alert is issued when ŷ goes above the threshold y_crit.
  - It is rescinded only after ŷ has stayed below y_crit for a continuous 48 h, so alerts last at least 48 h (pp. 3, 6).
- **Testing:** pseudo-prospective cross-validation. The authors describe this as "strictly speaking, hindcasting". The data 1 month either side of the test eruption is held out from feature selection and training. There is one model per held-out episode, five in total (pp. 3, 6). Metrics: [[forecast-evaluation-roc-auc]].

## Results
- **At y_crit = 0.8** (80 of 100 trees predicting an eruption), the models gave advance warning for **5 of the 7 eruptions**, which is **4 of the 5 episodes** (p. 3, Fig. 2c):
  - 2012-08-04: alert 16 h before, "several days after an alert raised on 1 August".
  - 2013-08-19: alert 75 h before.
  - 2013-10-03: 7 h. 2013-10-08: **missed**. 2013-10-11: 70 h.
  - 2016-04-27: **missed entirely**.
  - 2019-12-09: **17 h** warning. The peak ensemble mean of 0.94 came 4 h before the eruption, and any threshold above about 0.94 would have missed it (Fig. 2a). The abstract's "at least four hours warning" fits this: every threshold up to the peak gives ≥ 4 h (our reading).
- **Alert statistics** (p. 4):
  - At 0.8: **58 alerts** covering **8.5%** of the study period. Five alerts contained eruptions, so the **eruption probability during an alert is 8.6%** (5/58).
  - At 0.93: 26 alerts covering 2.5% of the time, with 15% eruption probability during an alert. But 2013-10-03 is missed.
  - Matching 5/7 eruptions by placing alerts at random would need 70% of the time on alert (p. 6).
  - MCC is 0.2–0.4 depending on y_crit, "a weak positive to moderate positive relationship" (p. 6).
- **Training only on earlier data:** four models were trained on data up to 1 month before episodes 2–5. Oct 2013 and Dec 2019 were anticipated at 0.8. Training on the 2012 eruption alone did not pick up Aug 2013 (p. 4). The main text does not state the outcome for 2016.
- **Overfitting demonstration:** a hand-picked two-node decision tree using RSAM maximum and the 4-h harmonic, fitted on all data with no cross-validation, issued 12 alerts. Those alerts contained 6 of 7 eruptions (2016 missed), with 55 days on alert and 50% eruption probability during an alert. The authors call it "superficially" better and likely "very poor" on future data (p. 5).
- **Sensitivity tests:**
  - Window length T_w from 12 h to 5 days: longer windows dilute the precursor and shorter ones make the model overconfident. 48 h was chosen.
  - Look-forward T_lf from 12 h to 5 days: confidence was highest at 48 h.
  - Undersampling ratio and RNG seed: robust.
  - Adding more eruptions raised model confidence *and*, unexpectedly, alert duration (p. 6).

## Precursors and interpretation
- **Significant features** (p. 2, Fig. 1d–g):
  - The RSAM Fourier coefficient for **40-min periodicity** was large before 4 of the 5 eruptive periods.
  - **RSAM maximum** and **4-h periodicity** were also large.
  - The gradient of 1/RSAM, which failure-forecast modelling uses to extrapolate eruption onset, was "less remarkable".
- **The precursor itself:** the 2019 eruption and both 2013 episodes were preceded by **RSAM bursts ("paroxysms") lasting about 4 h, overlaid by a 40-min oscillation** (p. 5, Fig. 2d).
- **Hypothesis:** the bursts record degassing instabilities and gas cycling in the hydrothermal system, modulated by transient sealing. The 4-h signal "could indicate rising magma into the lower conduit, which further charges the hydrothermal fluids". The authors say this is consistent with three observations: dome extrusion after 2012, high SO₂ after 2013 and 2019, and lava sightings after 2019 (p. 5). **Presented as a hypothesis, not demonstrated.**
- **Why 2016 was missed:**
  - The 40-min and 4-h periodicities were much weaker, and tremor was low before and after the event (p. 4).
  - The 2016 ejecta showed hydrothermal mineralization, a hydraulic seal and no magmatic material. The authors interpret it as "a pure hydrothermal explosion of trapped meteoric fluids, without any increased injection of fluids into the system from below" (p. 4).
  - Their lesson is that data-driven models "only anticipate eruptions with precursors similar to those seen before". One proposed remedy is adding precursors from other volcanic systems, while checking that a volcano's unique signals are not diluted (p. 4). This is the idea [[ardid-dempsey-2025-transfer-learning]] later develops (see [[eruption-precursor-ergodicity]]).

## Operational context
- New Zealand's Volcanic Alert Level (VAL) runs from 0 to 5. Twenty-four days before the 2019 eruption, Whakaari was assessed at VAL 2, the highest level for a volcano not in eruption. The VAL describes the current state and is not a forecast (p. 2).
- Expert elicitation estimated an 8–14% eruption likelihood for the 4 weeks from 2019-12-02, the 50th–84th percentile range of the panel's estimates (p. 2).
- After past phreatic eruptions, the alert level jumped from 1→2, 1→3 and 2→4 on similar data, which the authors use to illustrate the heuristic nature of the VAL (p. 2).
- Advantages claimed for the model:
  - Speed: under a minute on a desktop to download data and forecast.
  - An objective estimate of eruption probability during an alert.
  - It needs only one station (p. 5).
- Drawbacks named:
  - Overfitting from software errors or data leakage.
  - Blindness to unfamiliar unrest.
  - Designer bias in the choice of classifier, station and windows.
  - Resourcing.
  - Who sets thresholds and who sees the output is "a societal debate" (p. 5).
- The authors state that the gold standard is evaluating a frozen model on future data (p. 5).

## Code and data
Processed tremor data and code: https://github.com/ddempsey/whakaari, **MIT licence** (p. 6). Raw data was downloaded with ObsPy from GeoNet (p. 5). Compare the CC BY-NC licence on the 2025 *Puia* library.

## Flags
- ⚠️ **Date of the fatal eruption.** The Introduction gives "**9 December 2019** at 2:11 p.m. (1:11 a.m. UTC)" (p. 2). Results (p. 2) and Methods (p. 5) give "**12 December 2019** at 01:11". The paper's own evidence supports 9 December: Figs. 1c and 2c place the eruption at Dec-09, and the retraining cutoff "up to 7 December 2019" lies 48 h before 9 Dec 01:11 (p. 6). The wiki uses 2019-12-09 01:11 UTC. The 12 December wording looks like a typo, but that is our inference.
- ⚠️ **Which model produced the alert statistics.** The 58-alert / 8.5% / 8.6% figures (p. 4) are given right after the cross-validation results. Figs. 2a–b, however, show "a model trained excluding the December 2019 eruption". The main text does not spell out which model, or which combination of the five models, those statistics come from.
- Description of eruption 2: "steam and mud eruption" (Results, p. 2) vs "minor steam eruption" (Methods, p. 5). A minor wording difference.

## Used by
[[whakaari]], [[transfer-learning-eruption-forecasting]], [[rsam-dsar]], [[forecast-evaluation-roc-auc]], [[eruption-precursor-ergodicity]], [[ardid-dempsey-2025-transfer-learning]], [[overview]].
