# Product: Sky Almanac

## Name
The brand name is **Sky Almanac** in every language (like a company name, it is not translated). The mascot keeps her name, **Doña Nube**, in every language.

## One sentence
The oldest tool of the countryside stitched to today's science: a paper almanac powered by 80 years of climate records, with an assistant that speaks the farmer's language, working in the field even without signal.

Hackathon: Kiroween 2026, category **Frankenstein** (we combine a 19th-century paper almanac, 80 years of reconstructed climate data, a historical planting simulator, and a talking assistant).

## The problem
Small farmers plant by traditional calendars ("the rains come in month X"). Climate change and El Niño made those fixed dates unreliable, and a false start of the rains (a few showers followed by a dry spell) kills the seed. Scientific planting-date analysis exists, but never reaches small farmers.

## Users
- **Primary:** small farmers, often with low literacy, poor connectivity and modest phones. Example persona: Rosa, maize farmer in Portoviejo, Manabí, Ecuador.
- **Secondary:** agricultural extension workers and cooperatives (they use the printed almanac in meetings).
- **Judges:** must be able to try everything in under a minute with "Try without an account".

## The golden rule: honesty
We never predict beyond the 7-day forecast. Everything else summarises what already happened.
- Never use words of certainty: no "it will rain", no "plant on day X". Always "in X of the last 10 years".
- Every number shows where it comes from and how many years it is based on.
- Show the bad years, not only the average (e.g. one dot per year).
- When there are few data or high variability, say so.
- Doña Nube only answers from the app's own calculations. She never invents facts.

## App flow
1. Splash with the animated logo.
2. Choose language (Duolingo style): Doña Nube asks "what language do you speak?" rotating through all languages. Phone language pre-selected.
3. Create account / sign in / **Try without an account**.
4. Plot location: GPS button, or country → region → district lists (names adapt per country: provincia/cantón in Ecuador, estado/município in Brazil, state/district in India).
5. Choose crop.
6. Main app with bottom navigation: **Home · Simulate · Tools · Chat**.

## Features
Must have:
- **Home / Your almanac:** "did the rains really arrive?" traffic light (real onset vs false start); rain onset dot strip (one dot per year since 1940, El Niño years highlighted); "years like this one" (analog El Niño / La Niña years); crop stage from degree-days; 7-day forecast; "how your climate changed" (recent decades vs the 1980s).
- **Planting simulator (the star feature):** pick a planting date, see how the crop would have done in each past year (10 plant icons for the last 10 years, green/red) and a comparison of several dates over all years.
- **Printed almanac:** an antique-style one-page summary, printable.

Should have:
- **Does your crop need water?** crop need (ET0 × crop coefficient) vs rain received this week.
- **Good time to spray?** hourly strip (green/amber/red) from rain and wind forecast.
- **Doña Nube:** a friendly cloud mascot that floats around the app, changes expression (happy, thinking, worried, celebrating) and gives tips in speech bubbles; plus a chat with quick-question chips; reads answers aloud.
- **Daily streak:** "Did it rain today in your plot?" (yes a lot / a little / no). Builds a habit and collects local ground-truth data.

Could have (only if time remains): accounts with sync; free-text AI chat when online.

Future (mention in the video, do not build): pest alerts, fungal disease risk, field logbook.

## Languages
Spanish (default), Kichwa, Portuguese, English, Hindi, Indonesian, Swahili. Chosen by where small farmers are, not by country size.
- Simple, neutral wording, plus a **regional vocabulary pack** (e.g. Ecuador: "fréjol", "choclo", "invierno" for the rainy season on the coast).
- Translations not reviewed by a native speaker must be marked as machine translated in the language list.

## Offline-first
After the first download (at home, in town or at the cooperative), the app must open and work in the field with no connection. Every feature either works offline from stored data or clearly tells the user what needs internet and when the data was last updated.

## Design
- Warm countryside palette: crop green `#3B6D11`, paper cream `#FBF6EC`, sun amber `#EF9F27`, rain blue `#378ADD`, earth brown `#854F0B`, alert red `#A32D2D`.
- Serif headings (antique almanac feel), sans-serif body for readability.
- Logo: a sun rising behind a green hill, a raindrop above and a sprout.
- Big touch targets, icons together with words, works on cheap phones.
- Reference images in `docs/design/`.
