---
type: index
created: 2026-06-17
updated: 2026-10-19
---

# Index

## Overview

- [[overview]] — living synthesis of the volcan-eye project (5 sources)

## Sources

- [[seed-manual-appendix-a]] — SEED v2.4 Appendix A: FDSN three-letter channel naming convention (1 source)
- [[jerk-beauducel-2025]] — Beauducel et al. 2025, Nat. Commun.: Jerk early-warning method at Piton de la Fournaise, 92% real-time success (1 source)
- [[ardid-dempsey-2025-transfer-learning]] — Ardid, Dempsey et al. 2025, Nat. Commun.: random-forest transfer learning across 24 volcanoes, AUC ≈ 0.8, explosive onsets only (1 source)
- [[ipgp-dc-data-access]] — Pardo & Satriano, IPGP-DC training deck: networks and DOIs, FDSN web services at ws.ipgp.fr, ObsPy examples (1 source)
- [[dempsey-2020-whakaari-forecasting]] — Dempsey et al. 2020, Nat. Commun.: single-station ML forecaster at Whakaari; 5/7 eruptions warned at 0.8 threshold; 2016 missed (1 source)

## Entities

- [[fdsn]] — International Federation of Digital Seismograph Networks; maintains SEED, StationXML and the web-service specs (2 sources)
- [[rer-station]] — Geoscope very-broadband STS-1 station 8 km from the Piton de la Fournaise summit; Jerk input (2 sources)
- [[piton-de-la-fournaise]] — basaltic volcano on La Réunion; 48 eruptions 1998–2023; outside the multi-volcano ML dataset; PF network (3 sources)
- [[geoscope]] — IPGP's global broadband network (code G), DOI 10.18715/GEOSCOPE.G (2 sources)
- [[ovpf-ipgp]] — Piton de la Fournaise volcano observatory; runs the Jerk alarm; PF network (2 sources)
- [[whakaari]] — phreatic/hydrothermal volcano, New Zealand; fatal eruption 2019-12-09; reference case for ML forecasting (2 sources)
- [[ipgp-data-center]] — IPGP Data Center (since 2011): archives and serves G, PF, GL, MQ, WI and XB; VOLOBSIS portal (1 source)
- [[webobs]] — open-source observatory monitoring system that hosts the Jerk module (1 source)

## Concepts

- [[seed-channel-naming]] — band · instrument · orientation codes, with the full band table (2 sources)
- [[What LHE channel at RER Station is]] — RER's LHE vs LME channels and LHE as a substitute Jerk input (3 sources + web metadata)
- [[jerk-signal]] — derivative of horizontal acceleration from fracture opening; physics, pipeline, performance, failure modes; contrast with ML (2 sources)
- [[horizontal-pendulum-seismometer]] — Eq. 1: recorded acceleration = translation + g·tilt + rotation (1 source)
- [[mass-position-channel]] — SEED "M" instrument code; LMN/LME calibration at RER and their availability (2 sources)
- [[transfer-learning-eruption-forecasting]] — multi-volcano random-forest forecasting for explosive onsets; pipeline, limits, Jerk comparison (2 sources)
- [[eruption-precursor-ergodicity]] — hypothesis that signals from many volcanoes approximate one volcano's history; evidence and caveats (2 sources)
- [[rsam-dsar]] — RSAM, MF, HF and DSAR seismic amplitude streams; not computable from 1 Hz LH channels (2 sources)
- [[fdsn-web-services]] — station, dataselect, event and availability services; URL anatomy; ObsPy; routing services (1 source)
- [[forecast-evaluation-roc-auc]] — ROC/AUC scoring; alert-based metrics; why the Jerk and ML AUCs aren't comparable (3 sources)
