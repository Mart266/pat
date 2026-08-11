# Test Tag Melbourne — Logger

Offline-capable web app for logging portable appliance testing on site, producing
client reports, and exporting the job as a zip.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app — logging, reports, exports, settings |
| `manifest.json` | Lets iOS install it as a home screen app |
| `sw.js` | Service worker; caches the app so it runs with no reception |
| `logo-letterhead-dark.svg` | App header artwork |
| `logo-letterhead.svg` | Report letterhead |
| `logo-stacked-dark.svg` | Stacked lockup, spare |
| `icon-192.png`, `icon-512.png` | App icons |
| `apple-touch-icon.png` | iOS home screen icon |

All files sit in the same folder, at the repo root.

## Deploying

1. Upload all files to the root of a **public** GitHub repo
2. **Settings → Pages** → Deploy from a branch → `main` → `/ (root)`
3. Visit `https://USERNAME.github.io/REPO/`
4. Open in **Safari** on the iPhone → Share → **Add to Home Screen**
5. Open it once from the icon while you have reception — that first load caches it

## Using it

**Job setup** — client, job reference, site, technician, instrument and calibration date.
Set once per job; stays until changed. *Start new job* clears the job fields but keeps
your tag sequence, remembered items and logged tests.

**Logging** — appliance name (tap a chip for a recent one), location, tag number,
Class 1 / Class 2 / Lead, then PASS or FAIL. A banner confirms each entry with an Undo.
Buttons lock briefly to stop double taps.

- Tag numbers advance by 1, keeping any prefix and zero padding: `T12V-400222` → `T12V-400223`
- The retest interval is read from the tag prefix (`T12V` = 12 months) and the next test
  date is calculated from the test date
- Test type is predicted from the last time that item was tested
- Inspection items all start ticked as passed; untick anything that failed
- Notes clear after each test, deliberately, so a fault note cannot carry to the next item
- Any logged test can be edited afterwards, including its result

**Failed items** — each failure appears in a follow-up list until a reason and action are
recorded. Up to eight photos per item, taken on the phone. Photos are stored as blobs in
IndexedDB, not in localStorage, so the practical limit is hundreds rather than about twenty.

**Reports** — Certificate of Conformance, Concise Test Report and Fail Report render as
print-ready pages. Choose Print, then save as PDF from the iOS share sheet.

**Export ZIP** — one file containing the CSV register and every photo, named by asset ID.
CSV alone is also available.

**Settings** — appearance (system, light or dark), restore an export, remembered item names
with per-item removal, storage usage with options to clear photos, and an about line.

**Restoring** accepts either file. A **zip** rebuilds records and photographs together, matching
photos to records by the asset ID in each filename. A **CSV** restores records only. Anything
already held is skipped, so importing the same file twice changes nothing.

This is also how to move data between two installs — export from one, restore into the other.
iOS gives each home screen icon its own storage, so a second icon starts empty.

## Storage

Two stores, both on the device:

- **localStorage** holds the test records, job setup and settings. Small and fast.
- **IndexedDB** (`ttm-photos`) holds the photographs as JPEG blobs.

Clearing Safari's website data erases both, and iOS can evict storage for sites left
unopened for long periods. Photos captured on an older version are migrated into
IndexedDB automatically the first time this version runs.

**Export the zip at the end of every job.** That file is the record; the phone is only
where you type.

## Updating

1. Upload the replacement `index.html`
2. Bump `CACHE_VERSION` in `sw.js`. Without this the phone keeps serving the cached copy
3. On the phone, force-quit the app and reopen it twice

Changing an icon or `logo.png` also needs the `CACHE_VERSION` bump, and iOS caches the
home screen icon at install — delete the icon and re-add it to pick up new artwork.

## Business details

The app ships with no business name, ABN, phone number or address in its source. Enter them
once under **Settings → Business details**; they are stored in the browser on that device and
appear on the reports from there. They are not part of this repository.

## Branding

Logos are vector SVG, traced from the supplied artwork. The dark letterhead runs in the app
header; the light letterhead sits on the reports. Icons are PNG, generated from the stacked
lockup.

## Scope

The app records what the tester decides. It does not measure anything, does not determine
pass or fail, and is not a substitute for the visual inspection and testing required under
AS/NZS 3760. Leakage current testing requires mains power; RCD trip-time testing and
microwave leakage testing are outside the capability of the Aegis Patrol Pro CZ5001.


### v63
- Multi-port sample values now generate one value per outlet in CSV exports.
- Added an in-app Detailed Test Report with per-item inspection details and per-outlet sample values for multi-port equipment.
