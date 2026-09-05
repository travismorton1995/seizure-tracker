# Seizure Log

A one-tap seizure timer and log, built to be opened by Quick Tap on a Pixel. All data
stays on the phone in browser storage — nothing is uploaded anywhere.

## Files

| File | What it does |
|---|---|
| `index.html` | The whole app — screens, timer, charts, import/export |
| `manifest.webmanifest` | Tells Chrome it's installable, sets name and icons |
| `sw.js` | Service worker — caches the app so it opens instantly with no signal |
| `icon-*.png` | App icons |

## Putting it on the phone

It has to be served over HTTPS for Chrome to install it as an app. GitHub Pages is the
least painful option and is free:

1. Create a repo (public or private, Pages works with both on a free account for public;
   private repos need Pro).
2. Upload the contents of this folder to the root of the repo.
3. Repo → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
4. Wait a minute, then open the URL it gives you on the Pixel **in Chrome**.
5. Chrome menu (⋮) → **Add to home screen** → choose **Install** (not "Create shortcut").
   The Install wording is what creates a real app entry — a shortcut won't show up in Quick Tap.
6. Settings → System → Gestures → Quick Tap → Open app → **Seizure Log**.

Once installed it works with the phone in airplane mode. To update it later, replace the
files in the repo and bump `CACHE = "seizure-log-v1"` in `sw.js` to `v2` so the phone
picks up the new version.

## How it behaves

- Opening the app starts the timer immediately. If you close it mid-seizure and reopen,
  it picks the same timer back up rather than starting over.
- The screen is kept awake while timing.
- "Cancel — don't log this" backs out of an accidental Quick Tap without saving.
- The auto-start toggle at the bottom of the log screen turns that behaviour off if you'd
  rather open the app to browse.

## Records

- **Export CSV** opens the Android share sheet when it can, so it can go straight to the
  vet by email. Otherwise it downloads.
- **Backup JSON** is the full-fidelity copy — use this one for moving to a new phone,
  since browser storage is wiped if you clear Chrome's site data.
- **Import** accepts either of the above, plus most hand-kept spreadsheets. It looks for
  a date/time column, a length column (`1:45` or plain seconds), a type column, and notes.
  Anything already in the log is skipped, so importing twice is harmless.
