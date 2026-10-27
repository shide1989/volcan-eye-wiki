---
type: source
created: 2026-10-19
updated: 2026-10-19
sources: ["raw/Data_access_at_IPGP-DC.pdf"]
tags: [ipgp, data-center, fdsn, web-services, obspy, training]
---

# Data access @ IPGP-DC (Pardo & Satriano)

A 91-slide training deck by Constanza Pardo and Claudio Satriano of the [[ipgp-data-center]] (IPGP-DC). It is licensed CC-BY 4.0. Origin: https://datacenter.ipgp.fr/doc/Data_access_at_IPGP-DC.pdf.

**Undated.** The latest example dates are from June 2021 (slides 56–58), and InSight is listed as "2016-2022" (slide 6). The PDF holds only "Part 1: Seismological and volcanological data" (slide 9). Citations below are slide numbers, which equal PDF page numbers.

## What it covers
- **The data center** (slides 3–7): its history, the services it provides, the networks it distributes and their DOIs. See [[ipgp-data-center]].
- **Formats** (slides 11–13): SEED (adopted by the [[fdsn]] in 1987), a short channel-naming table and FDSN StationXML. See [[seed-channel-naming]].
- **Web services** (slides 15–88): station, dataselect, event and availability. It also covers federated routing services and other RESIF/IRIS/EIDA services, and gives examples with curl/wget, ObsPy and the IRIS Fetch scripts. See [[fdsn-web-services]].
- **Volcano Reports web service** (slides 89–90): `https://ws.ipgp.fr/volcano-reports/`.

## Key facts
- IPGP's FDSN web services are at `https://ws.ipgp.fr/fdsnws/...`. They offer station, dataselect and event; availability was marked "(soon)" (slide 22). ObsPy has an `IPGP` shortcut (slide 51).
- The deck gives a DOI for each network (slide 7):

| Network | DOI |
|---|---|
| G ([[geoscope]]) | 10.18715/GEOSCOPE.G |
| GL (Guadeloupe) | 10.18715/guadeloupe.GL |
| MQ (Martinique) | 10.18715/martinique.MQ |
| PF ([[piton-de-la-fournaise]]) | 10.18715/reunion.PF |
| XB (InSight) | 10.18715/SEIS.INSIGHT.XB_2016 |
| WI (Antilles arc) | 10.18715/antilles.WI |

- **Worked example at Piton de la Fournaise** (slides 45–52). A script finds stations within 3 km of the main crater (−21.244384, 55.714093). It uses `maxradius=0.027`°, with the note "1 degree = 111 km". It then downloads EH?/HH? data for 2019-12-01 00:00–01:00. The output lists stations BON, BOR, ENO, FJS, FLR and FOR in network PF, but the listing is truncated (slide 50).
  - Station BON (−21.23971, 55.70921, 2552 m) records HH channels at 100 Hz. Its sensor was a Güralp CMG-3ESPCDE 100S in all periods except 2015-06-17 to 2016-04-20, when a CMG40T 60 s was installed (slide 47).

## Points to note
- The channel-naming table on slide 12 is shortened ("non exhaustive"). It differs from [[seed-manual-appendix-a]] in ways that matter. See the note in [[seed-channel-naming]].
- The PF network DOI here (10.18715/reunion.PF) is different from the DOI the Jerk paper cites for OVPF data (10.18715/REUNION.OVPF). ✅ Resolved via DataCite: the PF network dataset is **part of** the OVPF observatory data collection. See [[ovpf-ipgp]].
