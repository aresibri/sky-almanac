# Structure

```
src/
  app/          App shell, routing, bottom navigation, PWA setup
  screens/      One folder per screen: splash, language, welcome, location, crop,
                home, simulator, tools, chat, print
  engine/       Pure calculation functions (owned by the electronics teammate):
                onset, dry-spells, probabilities, analog-years, degree-days,
                water-balance, spray-window, trends, simulator, nube-answers
  data/         Static data: oni.json, crops.json, regions (Ecuador lists bundled)
  services/     Everything that touches the network or storage: open-meteo, geocoding,
                db (Dexie), sync
  nube/         Doña Nube: mascot component, expressions, speech bubbles, voice
  i18n/         Locale files: es, qu-EC (Kichwa), pt, en, hi, id, sw, plus regional
                vocabulary packs
  ui/           Shared components: cards, buttons, dot strip, plant icons, traffic light
tests/          Mirrors src/; property-based tests next to the unit tests of the same module
docs/design/    Screenshots of the prototypes, used as design reference
```

## Conventions
- Screens never call the network directly: they use `services/`. Screens never compute climate statistics: they call `engine/`.
- Ownership to avoid Git conflicts: `engine/` and `nube/` answer logic belong to the electronics teammate; `app/`, `screens/`, `services/`, `i18n/` belong to the computer science teammate. Touch the other's folder only after agreeing.
- File names in kebab-case, React components in PascalCase.
