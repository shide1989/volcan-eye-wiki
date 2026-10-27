---
type: concept
created: 2026-10-13
updated: 2026-10-19
sources: ["raw/SEEDManual_V2.4_Appendix-A.pdf", "raw/s41467-025-66256-z.pdf", "raw/Data_access_at_IPGP-DC.pdf"]
tags: [rer, geoscope, channel, lhe, lme, jerk]
---

**LHE at RER is the east-west ground speed, recorded once per second by a very sensitive seismometer.**

The name breaks down like this (SEED naming rule, see [[seed-channel-naming]]):

- **L** means long period, about 1 sample per second, so it is tuned to slow movements, not quick shakes.
- **H** means high-gain seismometer, the main "sensitive" output.
- **E** means the East-West direction. LHN is North-South and LHZ is vertical.

_Letters are read by position._ In slot 1, `H` would mean "High Broad Band" (80–250 Hz). It means high-gain seismometer only in slot 2. Likewise `M` means mass position only in slot 2. In slot 1 it is Mid Period. `E` is allowed because RER's azimuth (90°) is within the manual's 5° tolerance. For M (mass position) channels the manual gives units as "M/S\*\*2 (usually)". ([[seed-manual-appendix-a]], p. 124)

What the RESIF metadata says:

- Sensor: Streckeisen STS-1, with new electronics (Metrozet E300) since 15 Sep 2010. The paper agrees: two STS-1H horizontal sensors and one STS-1V, with STS1-E300 and Q330HR "since 2010" ([[jerk-beauducel-2025]], p. 6). Station details: [[rer-station]].
- Output: ground velocity in m/s, 1 Hz, azimuth 90° (due east), horizontal.
- Open data periods: 1990-07 to 2003-02, then a gap, then 2004-07 to now (location code "00"). There is also a 9-day gap in Sep 2010.
- Station position: lat -21.1712, lon 55.7399, 834 m altitude. Matches the paper (21.17120°S, 55.73986°E, 834 m).

**LHE vs LME.** LME is the same sensor and the same direction, but a different output. M means "mass position": where the sensor's internal weight sits. That signal follows very slow tilt or push of the ground, which is what the Jerk method needs. LHE is the normal "how fast is the ground moving" output. The [[jerk-signal]] paper used LME/LMN in real time and **used LHE/LHN only to calibrate them** ([[jerk-beauducel-2025]], p. 6). For eruptions before 2010, when no POS signal existed, it converted LHE/LHN to acceleration and applied the same processing (p. 6). On RESIF, LME is open only for 1999-07 to 2003-02, and the paper says post-2010 LM\* data is available on request only (p. 7). All three claims are now ✅ verified against the paper. More on M channels: [[mass-position-channel]].

Bottom line: LHE is our usable open substitute for Jerk's input, not the same signal. The paper's own pre-2010 workaround supports the approach we planned. One caveat from the paper: the velocity-to-acceleration conversion "can be properly done only in post-analysis conditions", because removing the instrument response needs a preliminary detrend (p. 6). A real-time version built on LHE would have to deal with this.

A quick note on wording: a channel does not _do_ anything. It _records_ one quantity. Asking "what does it measure, in which direction, how often" gets a sharper answer.

**Not verified:** I did not check the Geoscope station page. The IRIS service blocks automated access, and plain curl to RESIF/IPGP is blocked from this environment. The metadata above came through a web fetch.

**Access path (2026-10-19):** [[ipgp-dc-data-access]] documents the IPGP endpoint for network G: `https://ws.ipgp.fr/fdsnws/{station,dataselect}/1/query`, or ObsPy `Client('IPGP')` (slides 22, 51). See [[fdsn-web-services]]. Querying RER through it is deferred to a later session.

Sources:

- RER channel metadata (RESIF): https://ws.resif.fr/fdsnws/station/1/query?net=G&sta=RER&cha=LHE,LME&level=channel&format=text
- SEED manual, Appendix A (channel codes): [[seed-manual-appendix-a]] (`raw/SEEDManual_V2.4_Appendix-A.pdf`)
- Jerk paper, Beauducel et al. 2025: [[jerk-beauducel-2025]] (`raw/s41467-025-66256-z.pdf`)