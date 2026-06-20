# Indoor Air Quality Monitor

A single-page dashboard for logging and interpreting indoor air-quality sensor readings. Enter values from a handheld or fixed IAQ meter and get a combined, weighted **risk score** with plain-language guidance.

**Live site:** https://seajaysec.github.io/air-quality/

## Features

- **Six pollutants** — CO₂, PM2.5, PM10, PM1.0, TVOC, and HCHO (formaldehyde), each with EPA/WHO/ASHRAE-referenced thresholds.
- **Health-grounded overall risk** (0–100) — follows real-world index design instead of a flat average (see below).
- **Per-sensor color spectrum** with a live cursor and status badge (Good → Very Unhealthy).
- **Contextual guidance** — messages adapt to CO₂ spikes and elevated PM2.5 (wildfire smoke).
- **Reading history** with a risk sparkline over the session.
- **Shareable links** — "Share current values" encodes readings into the URL so you can send or bookmark a snapshot.
- Touch-friendly sliders, mobile responsive, dark UI. No build step, no dependencies.

## Usage

Open the live site, or just open `index.html` locally in any browser. Type a value or drag a slider for each sensor; the overall score and advice update live.

Prefill via URL parameters:

```
index.html?co2=460&pm25=26&pm10=33&pm1=15&tvoc=0.337&hcho=0.006
```

## Deployment

The app is a static `index.html` published with GitHub Pages via the workflow in `.github/workflows/pages.yml`. Pushes to `main` redeploy automatically.

## How the overall risk is calculated

The overall score is **not** a simple average of the sensors — averaging lets a
single dangerous pollutant hide behind several clean ones (e.g. one "Very
Unhealthy" PM2.5 reading averaging out to "Low Risk"). Instead the model
borrows from two established real-world indices:

1. **Per-sensor sub-index (continuous, 0–100).** Each reading is converted with
   piecewise-linear interpolation between its concentration breakpoints, the way
   the **US EPA AQI** computes pollutant sub-indices. Each severity tier occupies
   a fixed 20-point band, so the number always matches the tier color.
2. **Dominant pollutant sets the floor.** The overall score is anchored to the
   worst health-relevant sub-index (the EPA AQI "responsible pollutant"
   principle). The overall category can therefore never be milder than the worst
   sensor.
3. **Cumulative load adds on top.** When several pollutants are elevated at once,
   a bounded, weight-adjusted bump is added above the dominant value, reflecting
   the additive philosophy of **Canada's Air Quality Health Index (AQHI)**.

**CO₂ is contextual.** It is a ventilation proxy (and not part of the EPA AQI),
and cooking causes large transient spikes, so CO₂ is excluded from the dominant
floor — it only contributes to cumulative load and never sets the overall
category on its own. Per-sensor weights (fine/ultrafine particulates count more)
apply to the cumulative term.

## Reference standards

Thresholds are based on EPA, WHO, and ASHRAE 62.1 guidance; the aggregation
method follows the US EPA AQI (dominant pollutant) and Canada AQHI (cumulative
risk). This tool is for awareness only and is not a medical or regulatory
instrument.

## License

[MIT](LICENSE)
