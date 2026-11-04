# Tech

## Stack
- **Vite + React + TypeScript** (strict mode).
- **vite-plugin-pwa** for an installable, offline-capable app (service worker).
- **Dexie** (IndexedDB) to store climate data, the plot, the streak and settings on the device.
- **i18next + react-i18next** for translations.
- **Leaflet** with OpenStreetMap tiles for the map (the list selector is the offline fallback).
- **Web Speech API** for Doña Nube's voice (speechSynthesis) and, when available, voice questions.
- Charts drawn with plain **SVG** in React components (no chart library).
- Printing with a dedicated print stylesheet and `window.print()`.
- **Vitest** for unit tests and **fast-check** for property-based tests.
- Deployed on **Vercel**.
- Accounts (only in the last spec): **Supabase** free tier. Until then everything is local and "Try without an account" is the default path.

## Data sources (all free, no key required)
- Historical daily weather since 1940: Open-Meteo Historical Weather API (`archive-api.open-meteo.com/v1/archive`): `precipitation_sum`, `temperature_2m_max`, `temperature_2m_min`, `et0_fao_evapotranspiration`.
- Forecast: Open-Meteo Forecast API: daily values for 7 days, hourly `precipitation_probability` and `wind_speed_10m`.
- Place search: Open-Meteo Geocoding API. Reverse geocoding from GPS: OpenStreetMap Nominatim (respect its usage policy: max 1 request per second, identify the app).
- El Niño: NOAA CPC Oceanic Niño Index (ONI), bundled as a static JSON file in `src/data/oni.json` and updated by hand.
- Crop parameters: FAO-56 crop coefficients and season lengths, stored in `src/data/crops.json`, with the source of every value. Values must be reviewed by an agronomist.

## Architecture rules
- **Offline-first:** fetch once, store in Dexie, compute on the device. Every stored dataset records when it was fetched; the UI shows "updated X days ago".
- **The engine is pure:** everything in `src/engine/` is pure functions (arrays and numbers in, arrays and numbers out). No fetch, no Dexie, no React, no Date.now() inside the engine.
- **No secrets in the frontend.** If an AI chat is added later, it goes through a serverless function and only when online.
- **All UI text goes through i18n.** No hard-coded strings in components. Every key must exist in all 7 locale files.
- **Every engine function has property-based tests.** Examples of properties: probabilities are always between 0 and 1; cumulative degree-days never decrease; shuffling the order of years never changes a probability; with zero rain the rains never "start"; results are identical online and offline.
- Engine parameters (onset thresholds, dry-spell length, success criteria) live in one config file, documented, so they can be adjusted after agronomist review.
- Keep dependencies to this list unless there is a clear reason; ask first.

## Team context
Two second-semester students (electronics and computer science) using Kiro for the first time. Explain decisions in simple terms, keep tasks small, and prefer clarity over cleverness. Code, comments, specs and docs in English.

## Commands
- `npm run dev`: start the dev server
- `npm test`: run all tests once
- `npm run build`: production build
- `npm run preview`: serve the production build (use it to test offline mode)
