# GF 74(A) Cash Examination — installable offline app

One folder, no server, no build step. Everything runs in the browser.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app — markup, styles, logic, and the embedded GF 74(A) Excel template |
| `exceljs.min.js` | The library that writes the .xlsx file (kept local so it works offline) |
| `sw.js` | Service worker — caches the app so it runs with no signal |
| `manifest.webmanifest` | Tells the phone the name, icon and colours to use when installed |
| `icon-*.png` | Home-screen icons |

## Publishing it

The app must be served over **https** (or `http://localhost`). Service workers are
refused on plain `http://` and on `file://`, so opening `index.html` by double-clicking
gives you the app but **not** the offline install.

Any static host works. The simplest is a drag-and-drop host — drop this whole folder in
and you get a URL immediately. GitHub Pages, Cloudflare Pages and Netlify all have free
tiers that do this. Point people at that URL.

## Installing on a phone

- **Android / Chrome** — an "Install this on your phone" bar appears at the top. Tap
  **Install**. (Chrome also offers *Install app* in its ⋮ menu.)
- **iPhone / Safari** — tap the **Share** button, then **Add to Home Screen**. iOS does
  not offer an automatic prompt, so the app shows the instruction instead.

After installing, open it from the home-screen icon. It launches full-screen and works
with no signal at all.

## Updating it

Replace the files on the host. The service worker's cache name carries a build number,
so a new upload replaces the old cache; installed copies pick up the change the next
time they are opened with a signal.

## What is stored where

Nothing leaves the phone. Saved examinations and the in-progress draft live in that
browser's own storage, on that device. There is no account, no server and no sync — so
export the .xlsx for anything that has to survive.
