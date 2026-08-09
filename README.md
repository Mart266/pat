# PAT Testing Logger — setup

An offline-capable web app for logging portable appliance tests on site, with CSV export.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app — layout, logic, styling |
| `manifest.json` | Lets iOS install it as a home screen app |
| `sw.js` | Service worker; caches the app so it runs with no reception |
| `icon-192.png`, `icon-512.png` | App icons |
| `apple-touch-icon.png` | iOS home screen icon |

All six files must sit in the same folder.

## Putting it on GitHub Pages

1. Go to github.com → **New repository**. Name it `pat` (or anything). Set it **Public** — Pages needs this on free accounts.
2. On the empty repo page choose **uploading an existing file**. Drag in all six files. Commit.
3. **Settings** → **Pages** → under *Build and deployment*, Source = **Deploy from a branch**, Branch = **main**, folder = **/ (root)**. Save.
4. Wait a minute or two, then visit `https://YOURNAME.github.io/pat/`

## Adding it to the iPhone

1. Open that URL in **Safari** (not Chrome — only Safari can install to the home screen on iOS)
2. Tap **Share** → **Add to Home Screen** → **Add**
3. Open it once from the new icon while you still have reception. That first load caches everything.

From then on it opens straight from the icon and works with no signal.

## Using it

- **Appliance** — type it, or tap a chip. Chips show the 12 most recent matching names; typing filters them. Up to 200 names are remembered.
- **Site** and **Location** — sticky. Set once, they carry to every following test.
- **Tag number** — advances by 1 after each test, keeping any prefix and zero-padding (`T12V-400222` → `T12V-400223`, `5339` → `5340`). Overwrite it any time to jump to a new roll.
- **Test** — Class 1 / Class 2 / Lead. Sticky.
- **Notes** — cleared after every test, deliberately, so a fault note can't carry onto the next item.
- **Export CSV** — opens the iOS share sheet. Save to Files or OneDrive, or mail it to yourself.

## Important

Data is stored in Safari on that one phone. Clearing Safari's website data will erase it, and iOS can evict storage for sites left unopened for long stretches.

**Export the CSV at the end of every day.** That file is the record; the phone is only where you type.

## Updating the app later

1. Upload the replacement `index.html`
2. Edit `sw.js` and bump `CACHE_VERSION` — `pat-logger-v1` → `pat-logger-v2`. Skip this and the phone will keep serving the old cached copy.
3. Export your CSV first, in case stored data doesn't survive the change.

## Scope

The tool records what you decide. It doesn't measure anything, doesn't determine pass or fail, and isn't a substitute for the visual inspection and testing required under AS/NZS 3760.
