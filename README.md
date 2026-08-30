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
