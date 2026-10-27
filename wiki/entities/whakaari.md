---
type: entity
created: 2026-10-15
updated: 2026-10-15
sources: ["raw/s41467-020-17375-2.pdf", "raw/s41467-025-56689-x.pdf"]
tags: [volcano, new-zealand, phreatic, hydrothermal]
---

# Whakaari (White Island), New Zealand

A volcano with an active hydrothermal system, offshore from New Zealand's North Island. It is a test case for machine-learning eruption forecasting.

## Facts from [[dempsey-2020-whakaari-forecasting]]
- **Station:** monitored in near real time by the GeoNet broadband station **WIZ**, about 1 km southeast of the main vents. A second station, WSRZ, did not cover every eruption in the study (pp. 2, 5).
- **2019 eruption:** at **2019-12-09 01:11 UTC** (2:11 p.m. local) the volcano erupted, killing or fatally injuring 21 of the 47 tourists and guides on the island (p. 2). ⚠️ The paper also gives "12 December 2019" in two places, see the source page.
- **Alert level before 2019:** Twenty-four days before the eruption it was at Volcanic Alert Level 2 of 5. Expert elicitation put the eruption likelihood at 8–14% for the 4 weeks from 2019-12-02 (p. 2).
- **Major impulsive episodes, 2011–2020:** Aug 2012 (phreatic), Aug 2013 (minor steam), Oct 2013 (three eruptions), Apr 2016 (phreatic, six events in 35 min) and Dec 2019. Minor activity included dome growth (Sep–Nov 2012), mud and ash eruptions (Jan–Apr 2013) and an ash emission (Sep 2016) (p. 5).
- **Precursor:** RSAM bursts lasting about 4 h with a 40-min oscillation before 2019 and both 2013 episodes. The authors' hypothesis is that magmatic fluids are charging the hydrothermal system (p. 5).
- **2016 eruption:** its precursor was weak. The ejecta indicate a purely hydrothermal explosion of trapped meteoric fluids with no magmatic ejecta (p. 4).

## Facts from [[ardid-dempsey-2025-transfer-learning]]
- **Pool and record:** it belongs to the **phreatic pool** (p. 9). Fig. 2g–i uses a 10-year Whakaari record.
- **AUC (Table 1, p. 5):** tailored ML model 0.89, generalized model 0.96, RSAM 6 h benchmark 0.86.
- **Generalized vs tailored:** the generalized phreatic model strengthened output before the 2016 eruption, which earlier tailored studies had found hard to anticipate (p. 5, Fig. 5b). For 2019, the generalized model "has not compromised performance of the tailored alternative" (p. 5, Fig. 5c). Fig. 5 labels the 2016 eruption phreatic VEI 1 and the 2019 eruption phreatic VEI 2.

## Consistency between the two sources
Both papers report that the 2016 eruption was hard for tailored models to anticipate. Dempsey 2020 missed it entirely. Ardid 2025 attributes the difficulty to "prior studies" and cites a 2022 paper by Dempsey et al. (ref. 28) that is not in `raw/`.

## Relevance to volcan-eye
Whakaari is the reference case for **explosive and phreatic**, hydrothermally driven forecasting. It contrasts with the effusive, dyke-fed [[piton-de-la-fournaise]] and its [[jerk-signal]].
