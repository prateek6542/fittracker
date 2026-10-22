# FitTrack PWA — beginner setup

A personal, offline-first fitness tracker built with plain HTML, CSS and JavaScript.

## Files
- `index.html`: app interface and all application logic
- `manifest.json`: installation metadata
- `sw.js`: offline cache after the first successful load
- `icon-192.png` and `icon-512.png`: app icons for installation

## Run locally (quick preview)
You can double-click `index.html` to preview most features. Browser restrictions mean PWA installation and service-worker offline caching require HTTPS or localhost.

## Publish free with GitHub Pages
1. Sign in or create a free account at https://github.com.
2. Create a new repository, for example `fittrack`.
3. Upload `index.html`, `manifest.json`, and `sw.js` to the repository root.
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select branch `main` and folder `/(root)`, then save.
7. Wait for GitHub Pages to publish the site. Open the URL shown in Pages settings (usually `https://YOUR-USERNAME.github.io/fittrack/`).
8. Open that URL in Chrome on Android, let the page load once while online, then open Chrome's menu and choose **Install app** or **Add to Home screen**.
9. Open FitTrack once while online so the service worker can cache the app. Then test airplane mode.
10. Export a JSON backup regularly from Settings → Export JSON.

## Use on Android
- Chrome is the simplest option.
- Keep the same published URL when using the app so the browser accesses the same local data.
- Do not clear Chrome site data for the app unless you have exported a backup.
- Browser data is not automatically synced between devices.

## Data and calculations
- Meals are stored by date, with calories and optional protein/carbs/fat.
- One weight entry is stored per date.
- Each workout is logged separately with its own name and manually entered calorie estimate. Daily steps are entered separately and use a rough estimate of about 0.04 kcal per step. Total activity calories = estimated steps calories + the sum of manually logged workout calories. Step-calorie estimates vary by body size, pace and terrain and are not exact measurements.
- Net calories = calories eaten minus the calories burned you entered. This is a simple logged figure, not total daily energy expenditure.
- Weekly calorie totals include seven calendar days; days without logged meals count as zero.
- The starting weight defaults to the first weight you save, unless you set a different starting weight.
- JSON import replaces current records. Export before importing if you need a rollback.
- Everything is stored in browser local storage. This is convenient, but not a guaranteed backup.

## Limitations of this starter
- No cloud sync, account login, reminders, photo logging, barcode lookup or automatic wearable integration.
- The manifest has no custom app icon yet; browsers may use a generic icon.
- CSV export combines meals, weights and activity into one file with a `record_type` column.

## Dashboard redesign
The modern dark dashboard uses the existing `fittrack-data-v1` localStorage key and existing meals, weights, activities and settings arrays. The dashboard is a visual/interface update; it does not clear local data. New settings for protein and step goals are added compatibly with defaults. Before deploying, review the package and test on a copy or test browser profile.

## Daily Coach tab (local, no AI API)
- The Coach tab accepts a plain-text daily log with one meal per line, for example `Breakfast: 3 whole eggs, 90 g Bonn brown bread`, plus optional `Steps: 10000`, `Workouts: Chest and triceps 150 kcal; treadmill 100 kcal`, and `Weight: 79.5 kg` lines.
- Choose **Review my day** first. Matched foods and estimates are shown for review; unmatched foods are flagged and excluded rather than guessed. Then choose **Confirm & save day** to save.
- Coach calculations use the food database embedded in `index.html`. It is a rule-based, offline feature and does not call an external AI service.
- Count-based portions use transparent rough assumptions in the preview (e.g. 50 g per egg, 40 g cooked per roti). For best accuracy, provide grams/ml.
- Saving adds one new meal entry per meal category and does not delete existing meals. If steps/workouts are provided, the date's activity values are updated; a provided weight replaces that date's weight entry. Avoid saving a day twice if you already logged the same meals.


## Master food database update (2026-10-22)

All nutrition values are copied from `master_food_nutrition_database(1).xlsx` supplied by the user and treated as per 100 g exactly as requested. Blank fields remain null/unknown. `Chicken tikka masala` and `Homemade protein cake` are flagged as recipe-required and are excluded from nutrition totals until a recipe is provided.

## Coach search keywords

- **High-protein oats**: high protein oats, high-protein oats, pintola high protein oats, pintola oats, protein oats, high protein oatmeal, oats
- **Protein powder**: protein powder, naturaltine yes protein, yes protein, yes protein powder, naturaltine protein, protein supplement powder
- **Peanut butter**: peanut butter, beast life peanut butter, beastlife peanut butter, beast life, peanut spread
- **Cheese**: amul cheese, amul cheese slices, cheese, cheese cubes, amul cheese variant
- **Pasta**: pasta, dry pasta, uncooked pasta, pasta dry, macaroni
- **Bread**: bonn bread, bonn brown bread, bonn bread brown, bread, brown bread, bread slice, bread slices, bonn
- **Oats, plain**: plain oats, regular oats, rolled oats, plain oatmeal, oatmeal, generic oats, oats
- **Pumpkin seeds**: pumpkin seeds, pumpkin seed, pepitas
- **Almonds**: almonds, almond, badam
- **Whole egg**: whole egg, whole eggs, egg, eggs, boiled egg, boiled eggs
- **Egg white**: egg white, egg whites, egg white only, egg whites only
- **Banana**: banana, bananas, kela
- **Potato**: potato, potatoes, boiled potato, boiled potatoes, aloo
- **Rice, white**: white rice, cooked rice, plain rice, steamed rice, rice, chawal
- **Chicken breast**: chicken breast, raw chicken breast, skinless chicken breast, chicken breast raw, chicken
- **Atta / wheat flour**: atta, wheat flour, whole wheat flour, chapati flour, roti flour, gehun atta
- **Moong dal**: moong dal, mung dal, green gram dal, yellow moong dal, cooked moong dal, dal, daal
- **Malka dal**: malka dal, masoor dal, red lentils, cooked masoor dal, lentils, dal, daal
- **Rajma**: rajma, rajma curry, kidney beans curry, red kidney beans curry
- **Paneer**: paneer, homemade paneer, full fat paneer, full-fat paneer, cottage cheese
- **Milk**: milk, cow milk, cow’s milk, cows milk, full fat milk, full-fat milk, regular milk, whole milk
- **Plain curd**: plain curd, curd, dahi, plain yogurt, plain yoghurt, unsweetened yogurt, unsweetened curd
- **Poha**: poha, flattened rice, beaten rice, chiwda
- **Soya chunks**: soya chunks, soy chunks, soya, soy chunks dry, nutrela soya chunks
- **Pomegranate**: pomegranate, pomegranate arils, anar, anar dana
- **Mango**: mango, mangoes, aam
- **Mosambi**: mosambi, sweet lime, sweet lime fruit, mausambi
- **Persimmon**: persimmon, persimmons, japanese persimmon
- **Peanuts**: peanuts, peanut, groundnuts, groundnut, moongphali, mungfali
- **Coffee, black**: black coffee, black coffee unsweetened, coffee black, plain black coffee, coffee
- **Green tea**: green tea, plain green tea, unsweetened green tea
- **Chicken tikka masala**: chicken tikka masala, tikka masala chicken, chicken tikka gravy — **FLAGGED: recipe required; macros unavailable**
- **Homemade protein cake**: homemade protein cake, protein cake, homemade cake, protein powder cake — **FLAGGED: recipe required; macros unavailable**
