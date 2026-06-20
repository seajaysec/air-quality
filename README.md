# Indoor Air Quality Monitor

A single-page dashboard for logging and interpreting indoor air-quality sensor readings. Enter values from a handheld or fixed IAQ meter and get a combined, weighted **risk score** with plain-language guidance.

**Live site:** https://seajaysec.github.io/air-quality/

## Features

- **Six pollutants** — CO₂, PM2.5, PM10, PM1.0, TVOC, and HCHO (formaldehyde), each with EPA/WHO/ASHRAE-referenced thresholds.
- **Weighted overall risk** (0–100) — fine and ultrafine particulates count more; CO₂ is weighted lower because cooking causes transient, non-harmful spikes.
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

## Reference standards

Thresholds are based on EPA, WHO, and ASHRAE 62.1 guidance. This tool is for awareness only and is not a medical or regulatory instrument.

## License

[MIT](LICENSE)
