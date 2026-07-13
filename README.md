# ClassFlow — Netlify PWA package

This folder is ready to deploy to Netlify as a Progressive Web App (PWA).
Once deployed, anyone can open the link on Android, tap "Add to Home Screen,"
and it behaves like an installed app — its own icon, full-screen, works offline
after the first load.

## Deploy to Netlify (pick one)

### Option A — Drag & drop (no account setup needed)
1. Go to https://app.netlify.com/drop
2. Drag this whole folder onto the page.
3. Netlify gives you a live URL immediately (e.g. `random-name-123.netlify.app`).
4. Optional: in Site settings you can set a custom subdomain.

### Option B — Netlify CLI
```
npm install -g netlify-cli
cd classflow-netlify
netlify deploy --prod
```

### Option C — Connect a Git repo
Push this folder to a GitHub repo, then in Netlify: `Add new site > Import an existing project`,
pick the repo. `netlify.toml` is already set up (publish dir = root, no build step needed).

## Installing it on Android like an app
1. Open the deployed URL in **Chrome** on the Android phone.
2. Tap the ⋮ menu → **"Add to Home screen"** (or Chrome may prompt automatically).
3. It installs with the ClassFlow icon and opens full-screen, no browser bar.

## What was added to your original HTML
- `manifest.json` — app name, icons, standalone display mode (makes it installable)
- `sw.js` — service worker that caches the app shell so it still opens offline
- `icons/icon-192.png` and `icons/icon-512.png` — generated app icons
- A few `<link>`/`<meta>` tags in `<head>` pointing to the manifest/icons
- A small script at the end of the page that registers the service worker

Your app's own logic (schedules, students, drag & drop, etc.) is completely untouched.

## Limitations vs. a real Play Store app
- It's not distributed through the Play Store — it's a website that installs like an app.
- It still needs an internet connection the first time it loads (to fetch Tailwind CSS
  from its CDN and the logo image); after that, the cached shell works offline.
- If you eventually want a real `.apk` for the Play Store, the Android Studio project
  I built earlier in this conversation is the one to use for that.
