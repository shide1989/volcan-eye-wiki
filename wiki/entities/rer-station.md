---
type: entity
created: 2026-10-13
updated: 2026-10-19
sources: ["raw/s41467-025-66256-z.pdf", "raw/Data_access_at_IPGP-DC.pdf"]
tags: [station, geoscope, rer, broadband, la-reunion]
---

# RER station ("Eastern River", La Réunion)

A very-broadband seismic station in the [[geoscope]] network (network code G). It sits at [[piton-de-la-fournaise]] and provides the only input to the [[jerk-signal]] alarm. Source: [[jerk-beauducel-2025]] (p. 6) unless noted.

- **Location:** 21.17120°S, 55.73986°E, 834 m. It is **8 km** from the volcano summit, at azimuth **N17**, so the summit lies in direction N197 as seen from the station.
- **Sensors:** two Streckeisen **STS-1H** horizontal sensors and one **STS-1V** vertical sensor, with a 360 s period. Their sensitivity meets very-low-noise standards.
- **Electronics:** since 2010, Metrozet **STS1-E300** feedback electronics and a 26-bit Quanterra **Q330HR** digitizer. RESIF metadata dates the E300 to 2010-09-15 (see [[What LHE channel at RER Station is]]).
- **Setting:** a well-insulated shelter in the middle of a 4 km EDF tunnel. The mean temperature varies by less than 0.5 °C per year. Earth and ocean tides dominate the acceleration, at about 2·10⁻⁶ m·s⁻² peak-to-peak on the horizontal components.
- **Channels used:** LMN/LME, the [[mass-position-channel]] at 1 Hz, for real-time Jerk. LHN/LHE are used for calibration and as the source data before 2010. Channel codes are decoded in [[seed-channel-naming]].
- **Data:** raw data at http://geoscope.ipgp.fr. POS data after 2010 only on request (p. 7). Open data is served by the [[ipgp-data-center]] through [[fdsn-web-services]]: `https://ws.ipgp.fr/fdsnws/...`, network `G`, station `RER` ([[ipgp-dc-data-access]], slide 22). The network DOI is 10.18715/GEOSCOPE.G (slide 7).
- **Cross-check of the distance:** from the deck's "main crater" coordinates (−21.244384, 55.714093; slide 46), a great-circle calculation gives RER at **8.56 km, azimuth N18**. The paper says 8 km, N17. *Derived here, not stated in either source.* The two reference points may differ.
- **History:** early electronics (before 2001) had a low signal-to-noise ratio, and the 1999 Jerk was missed (p. 3). Maintained by [[ovpf-ipgp]] staff, with technical help from Geoscope.
