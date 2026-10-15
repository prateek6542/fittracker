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
10. Export a JSON backup regularly from Today → Export JSON.

## Use on Android
- Chrome is the simplest option.
- Keep the same published URL when using the app so the browser accesses the same local data.
- Do not clear Chrome site data for the app unless you have exported a backup.
- Browser data is not automatically synced between devices.

## Data and calculations
- Meals are stored by date, with calories and optional protein/carbs/fat.
- One weight entry is stored per date.
- Daily calories burned are manually entered with optional steps and activity notes.
- Net calories = calories eaten minus the calories burned you entered. This is a simple logged figure, not total daily energy expenditure.
- Weekly calorie totals include seven calendar days; days without logged meals count as zero.
- The starting weight defaults to the first weight you save, unless you set a different starting weight.
- JSON import replaces current records. Export before importing if you need a rollback.
- Everything is stored in browser local storage. This is convenient, but not a guaranteed backup.

## Limitations of this starter
- No cloud sync, account login, reminders, photo logging, barcode lookup or automatic wearable integration.
- The manifest has no custom app icon yet; browsers may use a generic icon.
- CSV export combines meals, weights and activity into one file with a `record_type` column.
