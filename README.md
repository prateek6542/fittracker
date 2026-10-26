# FitTrack Fitness Upgrade — Test Build

This ZIP is a **testable update**, not a live deployment. It is based on the latest available `FitTrack_Master_Food_Database_Coach_Update.zip` project files inspected for this task.

## Included features

1. **Smart daily dashboard** — retains the existing daily calorie/protein/steps/activity dashboard and adds one-tap buttons for saved meal templates.
2. **Weight trend & moving average** — weight chart now overlays the daily weights with a dashed trailing 7-calendar-day average. Missing weigh-in dates are ignored rather than treated as zero.
3. **Saved meals & one-tap logging** — use **Save** beside a logged meal to store a reusable template. In Food, templates can be added to the selected date with one tap; the Home dashboard also shows quick-add buttons. Adding a template creates a new meal entry and does not modify the original.
4. **Weekly fitness report** — reports weekly calories, average intake and protein on meal-logged days, average weight, activity burn, average steps on activity-recorded days, and calorie/protein target-day counts. Daily breakdown includes macros and activity.

## Data preservation

- Keeps the existing `localStorage` key: `fittrack-data-v1`.
- Keeps existing `meals`, `weights`, `activities`, and `settings` structures.
- Adds only an optional `savedMeals` array inside the same data object. Existing data without this property loads with an empty saved-meal list.
- Keeps the existing food database and Coach functionality.
- Updates the service-worker cache name so the browser can fetch the new app files. This does **not** delete localStorage records; it clears only old Cache Storage entries during service-worker activation.

## Files

- `index.html` — updated UI and feature logic
- `sw.js` — updated cache version
- `manifest.json`, `food_database.json`, `icon-192.png`, `icon-512.png` — carried forward unchanged

## Local test checklist

1. Make a backup from the current FitTrack app before testing.
2. Extract this ZIP into a **separate test folder**; do not replace files on the live GitHub Pages branch yet.
3. Open the test build using a local static server (recommended) or test in a separate browser profile/site copy.
4. Confirm existing meals, weights, activity records, settings, and Coach behavior still work.
5. Log weights on several dates; check that the chart shows daily points and a dashed average line. Confirm dates without weights are not shown as zero.
6. Save a logged meal as a template, add it to another date, and confirm the original entry remains unchanged.
7. Check weekly totals against the entries for the selected week, and verify empty days are not included in meal-day average calculations.
8. Export a JSON backup after testing. Only consider live upload after you approve the test results.

## Validation performed here

- JavaScript syntax checked with Node.js (`node --check`).
- Static inspection confirms the original storage key is unchanged and existing data arrays are still used.
- Full interactive browser testing against your real localStorage data has **not** been performed in this environment. Please test with a backup before any live update.
