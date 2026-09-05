# Seizure Log — notes for Claude

This is a single-file PWA (`index.html`) with a service worker (`sw.js`) that
caches the app for offline/instant-open use on a phone. There's no build step —
what's in the repo is what gets served.

## Always bump the cache version

`sw.js` uses a cache-first strategy keyed on `CACHE = "seizure-log-vN"`. The
phone's service worker keeps serving the old cached files until that constant
changes — a code change that doesn't bump it will look like it "didn't work"
when someone reinstalls/reopens the app, even though the repo is correct.

**Whenever you change `index.html`, `manifest.webmanifest`, or any cached
file, bump `CACHE` in `sw.js` to the next version** (`v1` → `v2` → `v3`, ...)
in the same commit. Do this automatically, without being asked.

## Files

- `index.html` — the whole app: screens, timer, charts, import/export.
- `sw.js` — service worker; cache-first fetch, `CACHE` version lives here.
- `manifest.webmanifest` — PWA install metadata.
- `icon-*.png` — app icons.

No frameworks, no bundler, no package.json — keep it that way unless asked.
