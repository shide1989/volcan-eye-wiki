---
type: concept
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-025-56689-x.pdf", "raw/s41467-025-66256-z.pdf", "raw/s41467-020-17375-2.pdf"]
tags: [evaluation, roc, auc, false-positive, method]
---

# Forecast evaluation: ROC and AUC

A **ROC curve** plots the true-positive rate, TPR = TP/(TP+FN), against the false-positive rate, FPR = FP/(FP+TN), as an alarm threshold sweeps from 0 to 1. **AUC** is the area under it: 0.5 means no skill and 1 means perfect discrimination with no false alarms. AUC summarizes skill without committing to one threshold.

## As used by Ardid, Dempsey et al. 2025
From [[ardid-dempsey-2025-transfer-learning]] (p. 9, Fig. 6):
1. A **pre-eruptive window** is defined (48 h before onset).
2. For each of 100 thresholds between 0 and 1, the model consensus is turned into an alarm (1 if above the threshold).
3. Outcomes are scored as follows:
   - TP: alarm inside the pre-eruptive window.
   - FN: no alarm in that window, *or* the first alarm comes after the window has started.
   - FP: alarm outside the window.
   - TN: no alarm outside the window.
4. TPR and FPR are computed for each threshold, and the curve is integrated to give AUC.

Evaluation is **pseudo-prospective**: test data is held out from feature selection and training. That is more realistic than a hindcast but not truly prospective (p. 9). The paper notes that the acceptable AUC for operational use depends on context, so it is "premature" to call AUC ≈ 0.8 good enough (p. 2).

## Alert-based metrics: Dempsey et al. 2020
[[dempsey-2020-whakaari-forecasting]] scores the *decision model* (issued alerts) instead of sweeping a ROC curve (pp. 3, 6):
- **Alert rule:** an alert is issued when the ensemble mean ŷ > y_crit. It is rescinded only after ŷ has stayed below y_crit for 48 h, so alerts last at least 48 h.
- **TP / FP:** a TP is an eruption inside an issued alert. An FP is an alert that contains no eruption.
- **Eruption probability during an alert:** TP / (FP + TP). At y_crit = 0.8 this is 5/58 = 8.6%. At 0.93 it is 15%.
- **Alert duration:** the fraction of the study period spent on alert. It is 8.5% at 0.8 and 2.5% at 0.93.
- **MCC (Matthews correlation coefficient):** ranges from −1 to 1, with 0 for guessing. It weights misses and false alarms equally. The model scored 0.2–0.4.
- **Model confidence:** the highest threshold that would still have raised an alert before an unseen eruption, max ŷ over [t_e − T_lf, t_e).

The ensemble mean is **not a calibrated probability** (2020, p. 6). The 2025 "consensus" plays the same role. These choices are a trade-off between alert duration, accuracy and specificity. The 2020 authors call the choice of threshold "a societal debate" (p. 5).

## As used by Beauducel et al. 2025
[[jerk-beauducel-2025]] reports AUC 0.85 for the [[jerk-signal]] alarm (2014–2023), with 0.1 nm·s⁻³ as the optimal threshold. Its counts (22 TP, 2 FN, 2 FP, 12 TN) appear to be **per event** (eruptions and intrusions). Ardid et al. score **per 10-min forecast step** inside or outside a 48 h window.

⚠️ **Not directly comparable.** Dempsey 2020's alert metrics form a third, alert-level scheme. The two AUCs (0.85 for Jerk, about 0.8 for the transfer-learning models) use different units of evaluation, different horizons and different eruption styles. Don't rank the methods on these numbers alone (our caution, not a claim from either paper).
