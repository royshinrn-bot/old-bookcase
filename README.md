# Old Bookcase

A quiet personal library for `.txt` books — a Progressive Web App designed to feel like an old leather-bound bookcase.

## Features

- Reads `.txt` files (auto-detects UTF-8 / EUC-KR / CP949 — works with old Korean text files)
- Paste-text option for older iPads without Files app access
- Page-flip reader (tap edges or swipe)
- 6 backgrounds (white, paper, sepia, mist, night, black)
- 5 fonts incl. Korean serif/sans
- Adjustable font size and line spacing
- Books and reading position saved locally
- **Works offline** after first load (Service Worker)
- **Installable to home screen** as a real app (PWA)

## Files

```
old-bookcase/
├── index.html        ← the app (single file)
├── manifest.json     ← PWA app definition
├── sw.js             ← service worker (offline cache)
├── icon-152.png      ← iPad
├── icon-167.png      ← iPad Pro
├── icon-180.png      ← iPhone (default Apple touch icon)
├── icon-192.png      ← Android / standard
└── icon-512.png      ← splash / store
```

## Deploy to GitHub Pages

### One-time setup

1. Create a new GitHub repo, e.g. `old-bookcase`. Make it **Public**.
2. Upload all 8 files above to the root of the repo.
3. Go to **Settings → Pages**.
4. Under "Build and deployment":
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` (or `master`), folder `/ (root)`
5. Save. Wait ~1 minute. GitHub will show a green checkmark and the URL:
   `https://YOUR_USERNAME.github.io/old-bookcase/`

### Install on iPad / iPhone

1. Open the URL above in **Safari** (must be Safari, not Chrome — only Safari can install PWAs on iOS).
2. Tap the **Share** button (square with arrow).
3. Scroll down and tap **"Add to Home Screen"**.
4. Confirm. The bookcase icon appears on the home screen.
5. Tap it — opens fullscreen, no Safari chrome, works offline from now on.

## Updating the app

When you change `index.html` or any file:
1. Push the new files to GitHub.
2. **Bump the cache version** in `sw.js`:
   ```js
   const CACHE_VERSION = 'old-bookcase-v2';   // was v1
   ```
   This forces installed copies to fetch the new files instead of serving stale cached ones.
3. Re-open the app on the iPad — the service worker will detect the new version on next launch.

## Notes on old iPads

- iOS 11.3+ supports Service Workers (offline mode).
- Older iOS (9, 10) will still work but **without offline support** — needs internet to load the first time. After that the browser cache may keep it around.
- All `.txt` reading happens client-side. No data leaves the device. No server needed.

## Local testing (optional)

If you want to test locally before pushing to GitHub:

```bash
cd old-bookcase
python3 -m http.server 8000
# Open http://localhost:8000 in any browser
```

Service workers require `https://` or `localhost` — they will not register from `file://`.
