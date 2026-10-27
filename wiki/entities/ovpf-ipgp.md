---
type: entity
created: 2026-10-13
updated: 2026-10-19
sources: ["raw/s41467-025-66256-z.pdf", "raw/Data_access_at_IPGP-DC.pdf"]
tags: [observatory, organization, ipgp, la-reunion]
---

# OVPF-IPGP

Observatoire Volcanologique du Piton de la Fournaise, part of the Institut de physique du globe de Paris. It monitors [[piton-de-la-fournaise]] and maintains [[rer-station]]. It runs the real-time [[jerk-signal]] alarm inside [[webobs]], with alarms checked by humans during maintenance and storms. It publishes continuous data at https://doi.org/10.18715/REUNION.OVPF. Source: [[jerk-beauducel-2025]] (pp. 2, 5–7).

Its seismic network is **PF**, distributed by the [[ipgp-data-center]] through the VOLOBSIS portal (http://volobsis.ipgp.fr). [[ipgp-dc-data-access]] gives the network DOI as **10.18715/reunion.PF** (slide 7).

✅ **Two DOIs, no contradiction (resolved 2026-10-19 via DataCite metadata):** the two are distinct, and one is part of the other.

| DOI | Cited by | DataCite title | Resource type | Year | Resolves to |
|---|---|---|---|---|---|
| 10.18715/REUNION.OVPF | [[jerk-beauducel-2025]] | Data collection of the volcanological observatory of Piton de la Fournaise | Datasets, products, collections and reports | 2021 | http://volobsis.ipgp.fr/ovpf |
| 10.18715/reunion.PF | [[ipgp-dc-data-access]] | Seismic, tiltmeter, extensometer, magnetic and weather permanent networks on Piton de la Fournaise volcano and La Réunion | Seismic, deformation, magnetic and weather Network | 2008 | http://volobsis.ipgp.fr/networks/detail/PF |

In DataCite, REUNION.OVPF `HasPart` reunion.PF, and reunion.PF `IsPartOf` REUNION.OVPF. In short, OVPF is the observatory's whole data collection and PF is its permanent-network dataset. DOIs are case-insensitive: DataCite stores them as `reunion.ovpf` and `reunion.pf`. Source: https://api.datacite.org/dois/10.18715/reunion.ovpf and https://api.datacite.org/dois/10.18715/reunion.pf (web metadata, not in `raw/`).
