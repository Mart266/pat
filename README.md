# Test Tag Melbourne — Logger

Offline-capable web app for logging portable appliance testing on site, producing
client reports, and exporting the job as a zip.

Test Tag Melbourne · ABN 36 246 545 097

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
recorded. Up to four photos per item, taken on the phone.

**Reports** — Certificate of Conformance, Concise Test Report and Fail Report render as
print-ready pages. Choose Print, then save as PDF from the iOS share sheet.

**Export ZIP** — one file containing the CSV register and every photo, named by asset ID.
CSV alone is also available.

**Settings** — appearance (system, light or dark), restore from a previously exported CSV,
storage usage with options to clear photos or remembered item names, and an about line.

Importing a CSV skips records already held, so importing the same file twice is safe.
Photos are not carried in a CSV, so a restore rebuilds records without their photographs.

## Storage

Data is held in the browser on that one device. Clearing Safari's website data erases it,
and iOS can evict storage for sites left unopened for long periods.

**Export the zip at the end of every job.** That file is the record; the phone is only
where you type.

## Updating

1. Upload the replacement `index.html`
2. Bump `CACHE_VERSION` in `sw.js`. Without this the phone keeps serving the cached copy
3. On the phone, force-quit the app and reopen it twice

Changing an icon or `logo.png` also needs the `CACHE_VERSION` bump, and iOS caches the
home screen icon at install — delete the icon and re-add it to pick up new artwork.

## Branding

Logos are vector SVG, traced from the supplied artwork. The dark letterhead runs in the app
header; the light letterhead sits on the reports. Icons are PNG, generated from the stacked
lockup.

## Scope

The app records what the tester decides. It does not measure anything, does not determine
pass or fail, and is not a substitute for the visual inspection and testing required under
AS/NZS 3760. Leakage current testing requires mains power; RCD trip-time testing and
microwave leakage testing are outside the capability of the Aegis Patrol Pro CZ5001.
