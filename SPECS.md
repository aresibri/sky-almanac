# Los specs para Kiro, en orden

**Cómo usar este archivo:** cuando toque un spec, crean un **Spec** nuevo en Kiro y pegan el texto del recuadro. Kiro escribe requisitos, diseño y tareas; ustedes lo leen, lo aprueban y Kiro hace las tareas. **Un spec a la vez por persona.**

| # | Spec | Quién | Semana |
|---|---|---|---|
| 1 | Base del proyecto y datos del clima | Ella | 1 |
| 2 | Motor de cálculo | Tú | 2 |
| 3 | Idioma, bienvenida y ubicación | Ella | 2 |
| 4 | Tu almanaque (inicio) | Ella + Tú | 3 |
| 5 | Simulador de siembra | Tú | 3 |
| 6 | Herramientas: agua y fumigación | Tú | 4 |
| 7 | Doña Nube y la racha | Las dos | 4 |
| 8 | Sin internet y almanaque impreso | Ella | 4 |
| 9 | Cuentas (solo si da tiempo) | Ella | 5 |

---

## Spec 1 · Project foundation and climate data

```
Create a spec for the foundation of Sky Almanac. Follow the steering files.

1. Project setup: Vite + React + TypeScript (strict), Vitest, fast-check, Dexie, i18next, following structure.md. Add a short README explaining how to run the project.
2. A climate data service in src/services/open-meteo.ts that, given a latitude and longitude, downloads daily precipitation, max and min temperature and ET0 from 1940-01-01 until yesterday from the Open-Meteo Historical Weather API, and the 7-day forecast (daily, plus hourly precipitation probability and wind speed) from the Open-Meteo Forecast API.
3. Store everything in IndexedDB with Dexie, together with the date it was fetched. If data for that location already exists, read it from the database instead of downloading again.
4. A temporary debug screen: with the coordinates of Portoviejo, Ecuador (-1.05, -80.45), show how many days were downloaded, the date range, and a simple SVG bar chart of total rainfall per year.
5. Bundle src/data/oni.json with the NOAA Oceanic Niño Index (one value per 3-month season since 1950) and a small function to classify each year as El Niño, La Niña or neutral.
6. Create two agent hooks: (a) when a file in src/engine/ is saved, run the tests; (b) when a locale file or a component with user-facing text is saved, check that every i18n key exists in all 7 locale files and report missing ones.
7. Tests for the data service using a small fake response (no real network in tests).

Explain the design and the tasks in simple terms: we are beginners.
```

---

## Spec 2 · Calculation engine

```
Create a spec for the calculation engine in src/engine/. Everything must be pure functions with unit tests and property-based tests (fast-check). Put all thresholds in one documented config file.

Input: arrays of daily values (date, rain mm, tmax, tmin, et0).

1. Rainy seasons: from the monthly climatology, detect whether the location has one or two rainy seasons per year and their typical window.
2. Rain onset per year: the first day in the season window where accumulated rain over 3 days reaches a threshold (start with 20 mm), not followed by a dry spell (start with 10 days under 1 mm) in the next 30 days. Return null for years where the season never started.
3. False start check for the current season: given the rain so far this season, return "not yet", "maybe a false start, wait" or "the season has started", using the same criteria.
4. Probabilities: from the onset dates of all years, return statements like "in 8 of 10 years the onset was between date A and date B" (the central 80%), plus the earliest and latest years.
5. Analog years: given the ONI classification, return the onset statistics restricted to El Niño years or La Niña years, and the difference with all years.
6. Trends: compare the median onset of 1981–1990 with the last 10 years, in days.
7. Degree-days: accumulated growing degree-days since a planting date for a given base temperature, and the crop stage from thresholds in src/data/crops.json.
8. Property-based tests, at least: probabilities always between 0 and 1; shuffling the order of years never changes the statistics; with zero rain the season never starts; accumulated degree-days never decrease; adding a rainy day can never make the onset later.

Our electronics teammate owns this module: explain each algorithm with an analogy to signal processing (thresholds, windows, debouncing).
```

---

## Spec 3 · Language, welcome and plot location

```
Create a spec for the onboarding flow, following the steering and the reference images in docs/design/.

1. Splash screen with the animated logo (sun rising, raindrop falling) and the tagline.
2. Language screen in Duolingo style: Doña Nube (static for now) asks "what language do you speak?" rotating through the 7 languages; a list of languages written in their own names (no flags); the phone language is pre-selected; big "Continue" button. The choice is saved and can be changed later from settings.
3. Locale files for es, qu-EC (Kichwa), pt, en, hi, id, sw. Mark machine-translated languages in the list until a native speaker reviews them.
4. Welcome screen: create account and sign in buttons (they only show a "coming soon" message for now) and a prominent "Try without an account" button that continues.
5. Plot location screen: a Leaflet map; a "Use my location (GPS)" button that gets the coordinates and fills country, region and district using reverse geocoding when online; and a manual path: search a place by name (online) or pick from bundled lists for Ecuador (provinces and cantons) when offline. Region labels adapt to the country (provincia/cantón, estado/município, state/district).
6. Crop screen: maize, rice, beans, peanut (from src/data/crops.json), with icons, using regional names from the vocabulary pack (e.g. "fréjol" in Ecuador).
7. After the crop is chosen, download the climate data with the service from spec 1, showing a friendly progress message.
```

---

## Spec 4 · Your almanac (home)

```
Create a spec for the home screen "Your almanac" and the bottom navigation (Home, Simulate, Tools, Chat), using the engine from spec 2 and the reference images in docs/design/.

Cards, top to bottom:
1. "Did the rains really arrive?" traffic light (red / amber / green) with a one-line explanation.
2. Rain onset dot strip: one dot per year, positioned by onset date, El Niño years highlighted, with the plain-language probability sentence below.
3. "Years like this one": the analog-years sentence for the current ENSO phase.
4. Crop progress bar with stages from degree-days (only if a planting date was entered).
5. Next 7 days with icons and one advice sentence.
6. "How your climate changed": the trend sentence.

Rules: every card shows "based on N years" and when the data was last updated; never use words of certainty; everything works from stored data.
```

---

## Spec 5 · Planting simulator

```
Create a spec for the planting simulator, the star feature.

Engine (pure functions with property-based tests):
1. Given a planting date and a crop, evaluate each past year: the year is "good" if there was no dry spell longer than the configured limit in the first 30 days, and the water supply (rain) covered at least the configured share of the crop need (ET0 × crop coefficient from crops.json) during flowering. Return per-year results and the reason when a year was bad.
2. Compare several planting dates and return the share of good years for each.

Screen:
3. Three suggested dates as chips plus a date picker.
4. Ten plant icons for the last 10 years (green = good, red = bad, with the year), animated one by one.
5. Horizontal bars comparing the dates over all years, highlighting the best one.
6. A plain-language sentence, e.g. "Planting around January 20, your maize would have done well in 86 of every 100 years."

Property-based tests: the share of good years is between 0 and 1; adding rain to a year can never turn a good year into a bad one; results do not depend on the order of years.
```

---

## Spec 6 · Tools: water and spraying

```
Create a spec for the Tools screen.

1. "Does your crop need water?": for the last 7 days, crop need = sum of ET0 × crop coefficient for the current stage; rain received = sum of rain. Show two bars, the difference in mm and an advice sentence. Use stored data and show when it was updated.
2. "Good time to spray?": from the hourly forecast, mark each hour from 6 am to 6 pm as good (no rain expected in the next hours, low wind), fair or bad, using thresholds in the engine config. Show a colored strip and the best window as a sentence. If the forecast is older than 24 hours or there is no connection, say so clearly instead of showing stale advice.
3. Engine functions are pure with property-based tests (e.g. more rain never increases the water deficit; an hour with rain is never "good").
```

---

## Spec 7 · Doña Nube and the daily streak

```
Create a spec for Doña Nube and the daily streak, following the reference images in docs/design/.

1. Mascot component: a cloud with a face and 5 expressions (happy, waving, thinking, worried, celebrating), a gentle floating animation, and speech bubbles. On each screen she moves to a position and says one contextual tip produced by the engine (e.g. worried when the crop needs water, celebrating when the simulator finds a good date). She can be minimised.
2. Answer engine (pure functions in src/engine/nube-answers.ts): answers the quick questions ("Can I plant now?", "What is the best date?", "Should I spray today?", "Will there be a drought?") only from the engine results, always with probabilities, in the selected language through i18n templates. Never invents facts.
3. Chat screen: chat bubbles, quick-question chips, and a "listen" button that reads the answer aloud with speechSynthesis in the selected language. A microphone button only if the browser supports speech recognition.
4. Daily streak: a card "Did it rain today in your plot?" (a lot / a little / no). Save the answer locally with the date, show the streak counter, and keep it for future sync.
5. Respect "reduce motion" settings: no floating animation when the user prefers reduced motion.
```

---

## Spec 8 · Offline mode and printed almanac

```
Create a spec for full offline support and the printed almanac.

1. Configure vite-plugin-pwa so the app is installable and opens with no connection after the first visit.
2. Offline banner: when there is no connection, show a small banner; every card shows when its data was updated; features that need internet (fresh forecast, map, place search, voice questions) explain it clearly.
3. When the connection returns, refresh the forecast and the latest days of history in the background.
4. Printed almanac screen: an antique-style one-page summary (logo, season, location and crop, onset probability, best planting date, El Niño note, climate change note, the honesty tagline) with a print stylesheet and a "Print" button.
5. A test plan to verify offline behaviour with `npm run build` + `npm run preview` and the browser's offline mode, and on a phone in airplane mode.
```

---

## Spec 9 · Accounts (solo si da tiempo)

```
Create a spec for optional accounts with Supabase (free tier).

1. Sign up and sign in with email (or phone if simple), keeping "Try without an account" as a first-class path.
2. When signed in, sync the plot, crop, settings and streak answers to Supabase; the app stays local-first and works offline, syncing when a connection is available.
3. No secret keys in the repository: use environment variables, and explain how to set them in Vercel.
```
