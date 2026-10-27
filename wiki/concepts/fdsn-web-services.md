---
type: concept
created: 2026-10-19
updated: 2026-10-19
sources: ["raw/Data_access_at_IPGP-DC.pdf"]
tags: [fdsn, web-services, obspy, stationxml, miniseed, data-access]
---

# FDSN web services

HTTP services, standardized by the [[fdsn]], for searching and downloading seismological data. Version 1.0 of the specification dates from 2013. Before it came, data was requested by CD-ROM (GEOSCOPE, before 2000), NetDC (1999–2016) and Arclink (2010–2019). Source: [[ipgp-dc-data-access]] (slide 15) unless noted.

## URL anatomy (slide 20)
`https://ws.ipgp.fr` / `fdsnws` / `dataselect` / `1` / `query?` — these parts are the base URL, service family, service name, service version and method. Query parameters are separated by `&`. In a shell, `?`, `=` and `&` must be escaped or quoted.

## The four services (slides 21–22)
| Service | Returns | At [[ipgp-data-center]] |
|---|---|---|
| fdsnws-station | metadata in FDSN StationXML (also `format=text`) | yes |
| fdsnws-dataselect | time series in miniSEED by default | yes |
| fdsnws-event | event parameters in QuakeML by default (also `format=text`) | yes |
| fdsnws-availability | time extents (`/extent`) or contiguous spans (`/query`) | "soon" (slide 22); examples use RESIF (slides 82–86) |

- `level=response` on station requests returns the full instrument response, which ObsPy can read with `read_inventory` / `get_response` (slides 27–33). `level=channel` lists channels with their sensor, scale and sample rate (slide 46).
- `nodata=404` makes an empty result return an HTTP error, so a script can detect it (slide 49).
- Query builders: `https://ws.ipgp.fr/fdsnws/station/1/builder` and `.../dataselect/1/builder` (provided by SeisComP3), plus the IRIS builders with the base URL changed. Not every data center supports every IRIS option (slides 34–36, 42–44).

## Clients
- **ObsPy:** `Client('https://ws.ipgp.fr')` or the shortcut `Client('IPGP')`. Use `get_stations`, `get_waveforms` and `get_events` (slides 29, 40, 51, 60).
- **IRIS Fetch scripts:** FetchMetadata, FetchData and FetchEvent, with `SERVICEBASE=http://ws.ipgp.fr` (slides 30, 41, 62).
- **curl / wget** (slides 28, 39, 59).

## Federated / routing services (slides 63–81)
These services tell you which data center holds a given set of data. The deck notes they are "not yet a FDSN standard" (slide 64).
- **eidaws-routing** (ORFEUS): `format=GET` returns ready-made per-station requests. It accepts only box selection, not circular (slide 66).
- **irisws-fedcatalog**: the `net` parameter is mandatory (slide 76).
- **ObsPy** `RoutingClient('eida-routing')` / `RoutingClient('iris-federator')`. ObsPy allows circular selection even with eida-routing (slide 78).

## Other services (slide 88)
- resifws/irisws timeseries: SAC, ASCII or PNG output, with optional filtering or deconvolution.
- timeseriesplot.
- eidaws-wfcatalog: waveform quality-control metrics.
- IRIS MUSTANG: noise PSD/PDF and spectrograms.
- IRIS PH5WS.

## Relevance here
This is the documented open path to [[geoscope]] network G data, including [[rer-station]]'s LH\* channels. See [[What LHE channel at RER Station is]]. Channel codes are decoded in [[seed-channel-naming]].
