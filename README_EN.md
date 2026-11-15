# Dj Ape1 — Windows 10/11 desktop app

Builds two files into `dist`: **DjApe1-Setup-2.2.1.exe** (installer) and **DjApe1-Portable-2.2.1.exe** (no install; data in `DjApe1-data` next to the exe).

## What's inside
- Native folders: no permission prompts, fast scanning, tags and durations read by the system, new files detected automatically.
- Library on disk (`library\library.json`) with atomic writes and automatic backups (last 5); a damaged file falls back to the newest healthy backup. Restore: Manage → Data → "Restore…".
- Windows integration: media keys, taskbar buttons, tray icon, close-to-tray, start with Windows, "Open with Dj Ape1".
- Full screen: the ⛶ button in the top bar (and F11) for the whole program; separate from the track full screen.
- Audio: sound card selection and Audiophile mode in the 🔊 Audio menu.
- **Smart playlists with rules** (✨ next to the ＋ of Playlists in the sidebar, or the ✨ in the top bar — works with the sidebar hidden): genre, artist, title, album, year, BPM, key (incl. harmonic match), duration, play count, last played, file; "all" or "any" rule. Edit with ⚙ Rules.
- **🔮 Next-track suggestion** (top bar): scores your library by harmonic key (Camelot), BPM, genre and recent plays; ▶ play, ⏭ queue next, ➕ add. Optional **Auto DJ** when the queue ends. Run key/BPM analysis for better suggestions.
- **🧠 Smart Mix** (top bar, or 🧠 Mix on any playlist): like Automix but smarter. Pick a source (library, playlist or the rules you set up), genres, BPM range, duration, **energy flow** (steady, rising, falling, wave) and **key harmony**. Every next track is chosen by key, BPM, genre, artist variety and what you played recently, and you see the quality of each transition. Play with crossfade or save as a playlist.
- **📚 Library** (top bar): one window for everything — status, folders, **Sync folders** (reconnect + new files + merge copies), add folder, import/export, duplicate cleanup, new library (with a backup).
- **Duplicates:** detected by name+size, by artist+title+length, and by title+length when the artist is missing. After every scan, new copies are merged automatically into the existing track (details, plays and playlists are kept). Files on disk are never deleted.
- **⧉ Mini player** (top bar, Ctrl+Shift+M or tray): small always-on-top window.
- **🎨 Themes:** 9 themes (Dark, Light, Midnight, Forest, Crimson, Violet, AMOLED, Sunset, Mint).

## Build
**GitHub:** create a private repository, upload *all* files including the hidden `.github` folder, then Actions -> **Build Windows** -> Run workflow; download the `.exe` files from **Artifacts**. Push a tag like `v2.2.1` to also create a Release.
**Locally:** install Node.js LTS, double-click `build.bat` (or `npm install` + `npm run dist`). `npm start` runs without building, `npm test` runs the tests.

## Troubleshooting
- "Cannot create symbolic link … privilege": Windows blocks symlinks. `build.bat` retries automatically without exe icon editing. For your own icon turn on Developer Mode, delete `%LOCALAPPDATA%\electron-builder\Cache\winCodeSign`, and rebuild.
- `dist\win-unpacked\Dj Ape1.exe` is a working app even if packaging fails.

## If GitHub Actions says "Could not read package.json"
The workflow now finds the project folder by itself. If it still reports that package.json is missing, not all files were uploaded. The repository front page should show: `.github`, `app`, `assets`, `build`, `tests`, `main.js`, `native.js`, `preload.js`, `package.json`, `README.md`. Upload the **contents** of the zip (after extracting it), not the zip file itself.

## If the app freezes or the window goes black
- Web lookup is now a polite background task: while music plays it does not redraw the list, saves less often and waits when the app is slow.
- If the page crashes or hangs, the app records it, restores the library by itself and reloads. If it hangs, it asks whether to wait or reload.
- A black window usually means a GPU problem: after 2 GPU crashes the app switches to software rendering automatically. You can also change it from the tray → "GPU acceleration".
- Diagnostics file: Manage → Data → "Diagnostics file → Show" (`diagnostics.log`). If it happens again, send me that file.
