# Spark

A tiny anti-procrastination tool. Instead of giving you unlimited ideas to browse (which just becomes a new way to stall), Spark gives you **one idea at a time**, three times a day, with a countdown and a limited number of attempts — so you either commit or the idea's gone.

## Files

- `index.html` — the app itself.
- `ideas.txt` — the list of starting ideas, plain text, one per line. Edit this in any text editor — no code or JSON needed.
- `settings.json` — default settings (timer length, attempts per slot, slot boundaries). Edit this to change the shipped defaults for everyone who uses this deployment.
- `README.md` — this file.

## How it works

- The day is split into three slots: **Morning**, **Afternoon**, **Evening** (boundaries are configurable — 12:00 and 17:00 by default).
- Each slot shows one "how to start" idea and a countdown timer (20 seconds by default).
- You can **Pause**/**Resume** the countdown at any time if you need a moment.
- You get a limited number of **attempts per slot** (5 by default), split between two buttons:
  - **Reroll (tamer)** — get a more normal, less weird idea.
  - **Not feeling it** — get a weirder, more absurd idea.
- Tap **I started** to lock in the idea for that slot. If the timer runs out and you're out of attempts, the slot is marked missed.
- Complete all three slots in a day to keep your streak going.
- Ideas don't repeat until the whole pool in `ideas.txt` has been used, then it reshuffles.
- Progress (today's ideas, attempts used, streak) and any settings changes you make are saved in your browser so they persist between visits.

No sign-up, no backend, no tracking — everything runs and stays in your own browser.

## Settings (in-app)

Tap the ⚙ icon in the top-right of the card to open Settings:
- Timer length (seconds)
- Attempts per slot
- Morning end hour / Afternoon end hour (evening runs from there to midnight)

Saving reloads the page and applies your changes immediately. These are stored per-browser and override the defaults in `settings.json`, so you don't need to edit any files to tweak them.

## Running it locally

Because `index.html` now fetches `ideas.txt` and `settings.json` with JavaScript, opening the file directly by double-clicking it (`file://...`) will usually **fail to load those files** — browsers block local file fetches by default. To test properly on your own machine, serve the folder with a simple local server, for example:

```
python3 -m http.server 8000
```

then open `http://localhost:8000` in your browser. (If `ideas.txt` fails to load for any reason, the app falls back to a small built-in list of 5 ideas so it still works.)

## Deploying to GitHub Pages

1. Create a new **public** repo on GitHub.
2. Upload `index.html`, `ideas.txt`, `settings.json`, and this `README.md` to the repo.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, set branch to `main` and folder to `/ (root)`, then save.
5. Wait about a minute — your site will be live at:
   `https://<your-username>.github.io/<repo-name>/`

GitHub Pages serves files over HTTP(S), so the `fetch()` calls to `ideas.txt` and `settings.json` will work correctly there — no local server needed once deployed.

## Customizing

- **Idea list**: edit `ideas.txt` in any text editor. One idea per line, in the format:
  ```
  Your idea text here | 3
  ```
  The number after the `|` is weirdness, 1–5 (5 = weirder, 1 = tamer). If you leave off the `| number` part entirely, it just defaults to weirdness 3. Lines starting with `#` are ignored, so you can use them as comments.
- **Defaults for everyone**: edit `settings.json` (`timerSeconds`, `maxAttempts`, `morningEnd`, `afternoonEnd`).
- **Your own settings**: use the in-app ⚙ Settings panel instead — no file editing needed, and it won't affect other people using the same deployed link.

## Notes

- Since state is saved per browser, opening the site on a different device or browser starts a fresh streak there — it isn't synced across devices.
- This is a static, multi-file app: no server, no database, no accounts.
