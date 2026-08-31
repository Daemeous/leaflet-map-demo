# Leafletting Map — Public Demo

A public, no-real-consequences demo of the leafletting canvassing tracker. Anyone who signs in with a Google account is treated as authorised (see `DISABLE_AUTH_CHECK` in `index.html`), so visitors can try the edit flow without being on a real `Authorised` list. It reads from a dedicated demo Google Sheet, never a live constituency's data.

This repo is a **thin deployment** — it has no local `core.js`/`styles.css` of its own; both load directly from the primary [leaflet-map](https://github.com/Daemeous/leaflet-map) repo (see that repo's README, "Shared assets", for what that means).

Live: **https://daemeous.github.io/leaflet-map-demo/**

---

## Other live deployments

| Constituency / area | Site |
|---|---|
| Stafford | https://daemeous.github.io/leaflet-map/ |
| South Hams | https://daemeous.github.io/south-hams/ |
| Burton & Uttoxeter | https://daemeous.github.io/burton-uttoxeter/ |
| Stone, Great Wyrley & Penkridge | https://daemeous.github.io/stone/ |
| Barnsley, Penistone & Stocksbridge | https://daemeous.github.io/barnsley/ |
| St Helens | https://daemeous.github.io/sthelens/ |
| Shipley + Keighley and Ilkley | https://daemeous.github.io/shipley/ |

Related project — **[Pothole Watch](https://github.com/Daemeous/stafford-potholes)**, same visual style, separate Sheet/Apps Script backend.

The pipeline that builds a real deployment's road/residence data and its Google Sheet + Apps Script backend lives in **[leaflet-pipeline](https://github.com/Daemeous/leaflet-pipeline)**, not in this repo.

---

## Repository contents

| File | Purpose |
|------|---------|
| `index.html` | Demo config (`DISABLE_AUTH_CHECK: true`, its own demo Sheet ID/Apps Script URL) plus a small inline snippet linking back to the read-only source spreadsheet |
| `sw.js` | Service worker (must stay same-origin, so every deployment keeps its own copy even though `core.js`/`styles.css` are shared) |

`core.js`/`styles.css` are **not** in this repo — see [leaflet-map](https://github.com/Daemeous/leaflet-map)'s README before changing app behaviour, since a push there updates this demo too.

---

## Demo-specific setup

The demo's Apps Script deployment must independently treat every signed-in user as authorised (`DEMO_MODE` script property — see `Pothole App/AppsScript.txt`'s / `Leaflet App/AppsScript.txt`'s comments in leaflet-pipeline for the equivalent flag), or saves will fail with "Not authorised" even though the frontend let the user try. `DISABLE_AUTH_CHECK` in `index.html` only relaxes the frontend gate, not the backend one.


---

## License

This project's own code (this frontend, and — in [leaflet-pipeline](https://github.com/Daemeous/leaflet-pipeline) — the data pipeline and Apps Script backends) is licensed under the **[PolyForm Noncommercial License 1.0.0](LICENSE)**: free to use, share, and modify for any non-commercial purpose, with attribution. Most of this repo (`core.js`/`styles.css`) is loaded from [leaflet-map](https://github.com/Daemeous/leaflet-map), which carries the same license. See [`LICENSE`](LICENSE) for the full text.

Copyright © Daniel Hodgkins.

That covers this project's own code only. The geographic data it displays comes from sources under their own separate licenses that explicitly permit commercial use (see Attributions below) — this project's non-commercial restriction doesn't, and legally can't, extend to that underlying data.

## Attributions

| Dependency | License | Notes |
|---|---|---|
| [Leaflet.js](https://leafletjs.com) | BSD-2-Clause | © Vladimir Agafonkin and contributors |
| [OpenStreetMap](https://www.openstreetmap.org/copyright) | [ODbL](https://opendatacommons.org/licenses/odbl/) | Map tiles and road data © OpenStreetMap contributors. Permits commercial use; requires attribution and share-alike for derivative databases. |
| OS Boundary-Line & OS Open UPRN | [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) | © Crown copyright and database right, Ordnance Survey. Permits commercial use; requires attribution. |
| [Papa Parse](https://www.papaparse.com) | MIT | CSV parsing |
| [Turf.js](https://turfjs.org) | MIT | Geospatial analysis |
| Google Identity Services | [Google Terms of Service](https://policies.google.com/terms) | Sign-in, loaded from Google's own servers at runtime |
| [Overpass API](https://overpass-api.de) | [Usage policy](https://dev.overpass-api.de/overpass-doc/en/preface/commons.html) | OSM data queries (used by leaflet-pipeline) |

