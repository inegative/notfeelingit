# Spark

A tiny anti-procrastination tool. Instead of giving you unlimited ideas to browse (which just becomes a new way to stall), Spark gives you **one idea at a time**, three times a day, with a countdown and a limited number of attempts — so you either commit or the idea's gone.

## Files

- `index.html` — the app itself.
- `ideas-home.txt` — starting ideas for when you're at home. Plain text, one per line.
- `ideas-work.txt` — starting ideas for when you're at work (quieter, no floor-sitting or loud announcing).
- `ideas-cafe.txt` — starting ideas for anywhere that's neither home nor work (a café, a library, etc.).
- `settings.json` — default settings (timer length, attempts per slot, slot boundaries). Edit this to change the shipped defaults for everyone who uses this deployment.
- `README.md` — this file.

## How it works

- The day is split into three slots: **Morning**, **Afternoon**, **Evening** (boundaries are configurable — 12:00 and 17:00 by default).
- At the start of each slot, you first pick **where you are**: Home, Work, or Café. This picks which idea file it draws from, so you never get an idea that doesn't fit where you are (no "sit on the floor" suggestion at work).
- You can change your mind and pick a different place before you start (a small "Change place" link) — it doesn't cost you an attempt.
- Once a place is picked, it shows one "how to start" idea and a countdown timer (20 seconds by default).
- You can **Pause**/**Resume** the countdown at any time if you need a moment.
- You get a limited number of **attempts per slot** (5 by default), split between two buttons:
  - **Reroll (tamer)** — get a more normal, less weird idea.
  - **Not feeling it** — get a weirder, more absurd idea.
- Tap **I started** to lock in the idea for that slot. If the timer runs out and you're out of attempts, the slot is marked missed.
- Complete all three slots in a day to keep your streak going.
- Each place has its own pool of ideas and doesn't repeat until that place's whole list has been used, then it reshuffles.
- Progress (today's ideas, attempts used, streak) and any settings changes you make are saved in your browser so they persist between visits.

No sign-up, no backend, no tracking — everything runs and stays in your own browser.

## Settings (in-app)

Tap the ⚙ icon in the top-right of the card to open Settings:
- Timer length (seconds)
- Attempts per slot
- Morning end hour / Afternoon end hour (evening runs from there to midnight)

Saving reloads the page and applies your changes immediately. These are stored per-browser and override the defaults in `settings.json`, so you don't need to edit any files to tweak them.

## Running it locally

Because `index.html` now fetches `ideas-home.txt`, `ideas-work.txt`, `ideas-cafe.txt`, and `settings.json` with JavaScript, opening the file directly by double-clicking it (`file://...`) will usually **fail to load those files** — browsers block local file fetches by default. To test properly on your own machine, serve the folder with a simple local server, for example:

```
python3 -m http.server 8000
```

then open `http://localhost:8000` in your browser. (If any idea file fails to load for any reason, the app falls back to a small built-in list for that place so it still works.)

## Deploying to GitHub Pages

1. Create a new **public** repo on GitHub.
2. Upload `index.html`, `ideas-home.txt`, `ideas-work.txt`, `ideas-cafe.txt`, `settings.json`, and this `README.md` to the repo.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, set branch to `main` and folder to `/ (root)`, then save.
5. Wait about a minute — your site will be live at:
   `https://<your-username>.github.io/<repo-name>/`

GitHub Pages serves files over HTTP(S), so the `fetch()` calls to the idea files and `settings.json` will work correctly there — no local server needed once deployed.

## Customizing

- **Idea lists**: edit `ideas-home.txt`, `ideas-work.txt`, or `ideas-cafe.txt` in any text editor. One idea per line, in the format:
  ```
  Your idea text here | 3
  ```
  The number after the `|` is weirdness, 1–5 (5 = weirder, 1 = tamer). If you leave off the `| number` part entirely, it just defaults to weirdness 3. Lines starting with `#` are ignored, so you can use them as comments.
- **Defaults for everyone**: edit `settings.json` (`timerSeconds`, `maxAttempts`, `morningEnd`, `afternoonEnd`).
- **Your own settings**: use the in-app ⚙ Settings panel instead — no file editing needed, and it won't affect other people using the same deployed link.

## Notes

- Since state is saved per browser, opening the site on a different device or browser starts a fresh streak there — it isn't synced across devices.
- If you're updating from an older version of this app (the one without the place picker), your browser's saved progress from before this update is reset once — after that, streaks and daily state track normally on the new version.
- This is a static, multi-file app: no server, no database, no accounts.
