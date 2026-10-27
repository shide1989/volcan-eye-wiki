---
type: concept
created: 2026-10-13
updated: 2026-10-19
sources: ["raw/SEEDManual_V2.4_Appendix-A.pdf", "raw/Data_access_at_IPGP-DC.pdf"]
tags: [seed, fdsn, channel-naming, seismology]
---

# SEED channel naming (band · instrument · orientation)

A seismic channel name has three letters. Each letter encodes one aspect of the instrument and its digitization. The convention is recommended by the [[fdsn]] but not required by SEED. Source: [[seed-manual-appendix-a]].

**Read by position.** The same letter means different things in different slots. `H` in slot 1 = High Broad Band. `H` in slot 2 = High Gain Seismometer.

## 1. Band code (sample rate · corner period)
| Code | Band type | Sample rate (Hz) | Corner period |
|---|---|---|---|
| F | — | ≥1000 to <5000 | ≥10 s |
| G | — | ≥1000 to <5000 | <10 s |
| D | — | ≥250 to <1000 | <10 s |
| C | — | ≥250 to <1000 | ≥10 s |
| E | Extremely Short Period | ≥80 to <250 | <10 s |
| S | Short Period | ≥10 to <80 | <10 s |
| H | High Broad Band | ≥80 to <250 | ≥10 s |
| B | Broad Band | ≥10 to <80 | ≥10 s |
| M | Mid Period | >1 to <10 | |
| L | Long Period | ≈1 | |
| V | Very Long Period | ≈0.1 | |
| U | Ultra Long Period | ≈0.01 | |
| R | Extremely Long Period | ≥0.0001 to <0.001 | |
| P | ~0.1–1 day | ≥0.00001 to <0.0001 | |
| T | ~1–10 days | ≥0.000001 to <0.00001 | |
| Q | >10 days | <0.000001 | |
| A | Administrative | variable | NA |
| O | Opaque | variable | NA |

Use the sample rate to choose the band. The period descriptions are approximate.

## 2. Instrument code (what is measured)

### Seismometer family
| Code | Instrument | Units |
|---|---|---|
| H | High gain seismometer | M, M/S or M/S\*\*2 |
| L | Low gain seismometer | M, M/S or M/S\*\*2 |
| G | Gravimeter | usually M/S\*\*2 |
| M | Mass position (see [[mass-position-channel]]) | usually M/S\*\*2 |
| N | Accelerometer | M, M/S or M/S\*\*2 |

Older accelerometer channels sometimes used L or G. N has been the FDSN convention since Aug 2000.

### Other families
| Code | Instrument | Units |
|---|---|---|
| A | Tiltmeter | rad |
| B | Creep meter | |
| C | Calibration input | |
| D | Pressure / infrasound / hydrophone | Pa |
| E | Electronic test point | |
| F | Magnetometer | T |
| I | Humidity | |
| J | Rotational sensor | |
| K | Temperature | |
| O | Water current | |
| P | Geophone | |
| Q | Electric potential | |
| R | Rainfall | |
| S | Linear strain | |
| T | Tide | |
| U | Bolometer | |
| V | Volumetric strain | |
| W | Wind | |
| X | Derived / synthetic | |
| Y | Non-specific | |
| Z | Synthesized beam | |

Units are left blank where this page has not recorded them. The full list is in [[seed-manual-appendix-a]] (pp. 124–129).

## 3. Orientation code

### Seismometers
| Codes | Meaning |
|---|---|
| Z N E | Traditional: vertical, north–south, east–west |
| A B C | Triaxial |
| T R | Transverse, radial (for formed beams) |
| 1 2 3 | Orthogonal components, non-traditional orientations |
| U V W | Optional components |

Use N/E only if the sensor is **within 5°** of north/east. Otherwise use 1/2. The true dip and azimuth go in blockette 52.

### Pressure (third letter = location, not direction)
| Code | Meaning |
|---|---|
| O | Outside |
| I | Inside |
| D | Down hole |
| F | Infrasound |
| H | Hydrophone |
| U | Underground |

## Typical GSN channel sets
EH\* 100 sps · BH\* 20 sps · LH\* 1 sps · VH\* 0.1 sps · plus LOG, SOH, ACE, LCQ, OCF.

## Note on the IPGP-DC summary table
[[ipgp-dc-data-access]] (slide 12) gives a shortened ("non exhaustive") version of these tables. It differs from the manual as follows. Use the manual tables above.
- It gives E and H the same rate range (≥80 to <250), and S and B the same range (≥10 to <80). It drops the corner period (<10 s vs ≥10 s) that tells each pair apart.
- It writes L as "=1" where the manual says ≈1.
- It labels instrument H as "High Gain and Short Period Seismometers" and N as "Strong Motion". The manual says *high gain seismometer* and *accelerometer*.
- Its orientation list adds `IO` (inside/outside) and `NONE`.

## Worked example
`LHE` = L (≈1 Hz) + H (high-gain seismometer) + E (east, within 5°). `LME` = same band, but the **mass position** output (see [[mass-position-channel]]). See [[What LHE channel at RER Station is]].
