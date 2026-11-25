# NIGHTMARE — Cinematic Hacker Prank Experience

A lightweight, mobile-first, completely harmless fake cyberattack simulation built with vanilla **HTML5**, **CSS3**, and **JavaScript**. Designed to create realistic cinematic suspense through 5 progressive stages before flipping into a friendly prank reveal.

## Safety & Privacy Guarantee

NIGHTMARE is strictly a visual simulation:
- **Zero real hacking or scanning**: All terminal readouts and diagnostic checks are scripted visual animations.
- **Zero device or file access**: Never accesses files, camera, microphone, contacts, or geolocation.
- **Zero tracking or external calls**: No analytics, no cookies, no backend, no external CDNs, and no third-party fonts or audio downloads.
- **Offline ready**: Uses a procedural Web Audio API synthesizer and a local Service Worker (`sw.js`) so the site keeps working even offline after initial load.

## Project Structure

```text
nightmare/
├── index.html                 # Main application shell and 5-stage semantic structure
├── manifest.webmanifest       # Mobile web app metadata
├── sw.js                      # Offline cache Service Worker (local assets only)
├── vercel.json                # Static deployment config + privacy headers for Vercel
├── .nojekyll                  # Disables Jekyll processing on GitHub Pages
├── .github/workflows/
│   └── deploy-pages.yml       # Automated GitHub Pages deployment workflow
├── assets/
│   └── icon.svg               # Vector application & favicon icon
├── css/
│   ├── base.css               # Design tokens, 100dvh layout, HUD controls
│   ├── effects.css            # Scanlines, vignette, safe alert wash, glitch bursts
│   └── stages.css             # Stage 1-5 layouts, countdown ring, reveal card
└── js/
    ├── audio.js               # User-gesture procedural Web Audio API sound engine
    ├── effects.js             # Canvas tactical grid & celebration confetti engine
    ├── fullscreen.js          # Explicit-click Fullscreen API handler with iOS fallback
    ├── stages.js              # Deterministic 5-stage narrative state machine
    └── main.js                # App initialization & keyboard/HUD bindings
```

## 1. Run Locally

Serve the project over HTTP (recommended so the Service Worker and Web APIs operate in a standard origin context):

### Using Python
```bash
cd nightmare
python -m http.server 8080
```
Then open `http://localhost:8080` in your browser.

### Using Node.js
```bash
cd nightmare
npx serve . -l 8080
```

## 2. How to Test the Experience

1. **Full cinematic flow**: Open `http://localhost:8080`. The simulation starts immediately without needing any click:
   - **Stage 1**: Initialization console (`[01]`–`[05]`) with typing animation and progress bar.
   - **Stage 2**: Simulated environment scanning messages advancing progress to `100%`.
   - **Stage 3**: Sudden blackout beat -> `WARNING` / `UNAUTHORIZED ACCESS DETECTED` + `10` to `0` countdown.
   - **Stage 4**: Red screen breach transition -> `SYSTEM BREACHED` -> `CRITICAL SECURITY ALERT`.
   - **Stage 5**: Friendly prank reveal (`JUST KIDDING! 😂`) + `"OKAY, YOU GOT ME 😂"` celebration button.
2. **Audio controls**: Sound starts muted (`SOUND OFF`) to comply with browser autoplay rules. Tap **SOUND OFF** (or press `M`) to enable procedural background ambience, terminal beeps, countdown klaxon, breach drop, and reveal fanfare. Tap **SOUND ON** anytime for silent mode.
3. **Fullscreen control**: Tap **FULLSCREEN** (or press `F`) to toggle native fullscreen via the Fullscreen API. On browsers where fullscreen is unavailable (such as iPhone Safari), the button hides cleanly while `100dvh` keeps the viewport full-bleed.
4. **Quick stage testing URL parameters** (for QA/preview):
   - `?fast=1` — Runs the entire 5-stage sequence ~4.5x faster.
   - `?stage=3` — Starts directly at Stage 3 countdown.
   - `?stage=5` — Starts directly at Stage 5 reveal.

## 3. Deploy & Get a Shareable Public URL

### Option A — Deploy to Vercel (Fastest)
1. Install and log into Vercel CLI (or use the Vercel web dashboard):
   ```bash
npm i -g vercel
vercel login
```
2. From the `nightmare` directory, run:
   ```bash
vercel --prod
```
3. Vercel prints your live HTTPS URL (for example, `https://nightmare-prank.vercel.app`) — copy and share it directly.

*No-CLI alternative*: Push this folder to GitHub, open [vercel.com/new](https://vercel.com/new), import the repository with Framework Preset set to **Other**, and click **Deploy**.

### Option B — Deploy to GitHub Pages
1. Create a new repository on GitHub and push this folder:
   ```bash
git init -b main
git add .
git commit -m "Initial NIGHTMARE release"
git remote add origin https://github.com/<your-username>/nightmare.git
git push -u origin main
```
2. On GitHub, open **Settings -> Pages**, set **Source** to **GitHub Actions** (the included `.github/workflows/deploy-pages.yml` deploys automatically on push to `main`).
3. Once the workflow finishes, your shareable public URL will be:
   `https://<your-username>.github.io/nightmare/`
