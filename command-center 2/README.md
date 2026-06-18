# Summer Command Center

A self-contained progressive web app. Deploy it once, install it like a native app, and your data stays protected on the device.

## What is in this folder

- `index.html` the entire app (HTML, CSS, JS in one file)
- `manifest.webmanifest` makes it installable
- `sw.js` service worker, caches the app so it loads offline
- `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`, `favicon.svg` app icons
- `vercel.json` sets the right headers for the service worker and manifest
- `README.md` this file

## Deploy to Vercel (recommended)

### Option A, GitHub then Vercel
1. Create a new GitHub repo and push every file in this folder to the root.
2. Go to vercel.com, New Project, import the repo.
3. Framework preset: Other. Root directory: leave as is. No build command, no output directory.
4. Deploy. You get a link like `command-center.vercel.app`.

### Option B, Vercel CLI
1. Install once: `npm i -g vercel`
2. From inside this folder: `vercel` then `vercel --prod`
3. Use the production URL it prints.

### Option C, drag and drop
Any static host works (Netlify drop, GitHub Pages, Cloudflare Pages). Upload the folder contents to the site root.

> The service worker and install only work over https or on localhost. Vercel gives you https automatically. Opening `index.html` straight from disk still runs the app, but without install or offline.

## Install it as an app

Open your deployed link, then:

- **iPhone or iPad (Safari):** Share, then Add to Home Screen.
- **Android (Chrome):** menu, then Install app, or tap the Install button in the top bar.
- **Mac or Windows (Chrome or Edge):** the install icon appears in the address bar, or use the gold + button in the top bar.

Once installed it opens in its own window with the target icon, no browser bar.

## How your data is protected

Three layers, all automatic:

1. **Local save.** Every change is written to the device immediately. Closing the app loses nothing.
2. **Protected storage.** On first open the app asks the browser to mark its data as persistent so it will not be cleared to free space. You can confirm this under the shield icon (top right): it should read "granted." If not, tap "Protect storage."
3. **Rolling snapshots.** The app keeps the last six snapshots automatically. Restore any of them from the shield icon if something goes wrong.

For an offsite copy or to move between devices, use Export under the shield icon. It downloads a JSON file. Import it on any other device to load the same data.

## One thing to know about multiple devices

Data lives on each device separately. If you use it on both a laptop and a phone, they do not sync on their own. Export from one and Import on the other to match them up. If you want true automatic sync across devices later, that needs a small cloud backend, which can be added.

## Updating the app

Edit `index.html`, change the line `const CACHE = 'command-center-v1';` in `sw.js` to `-v2`, and redeploy. The version bump tells installed copies to pull the new version. Your saved data is not touched by updates.
