# Not Feeling It

A tiny anti-procrastination tool. Instead of giving you unlimited ideas to browse (which just becomes a new way to stall), Spark gives you **one idea at a time**, three times a day, with a countdown and a limited number of attempts — so you either commit or the idea's gone.

## How it works

- The day is split into three slots: **Morning** (before 12:00), **Afternoon** (12:00–17:00), **Evening** (after 17:00).
- Each slot shows one "how to start" idea and a 20-second timer.
- You get **5 attempts per slot** total, split between two buttons:
  - **Reroll** — get a tamer, more normal idea.
  - **Not feeling it** — get a weirder, more absurd idea.
- Tap **I started** to lock in the idea for that slot. If the timer runs out and you're out of attempts, the slot is marked missed.
- Complete all three slots in a day to keep your streak going.
- Ideas don't repeat until the whole pool (30 of them) has been used.
- Progress (today's ideas, attempts used, streak) is saved in your browser so it persists between visits.

No sign-up, no backend, no tracking — everything runs and stays in your own browser.

## Running it locally

Just open `index.html` in any modern browser (Chrome, Edge, Safari, Firefox). No build step, no dependencies to install.

## Deploying to GitHub Pages

1. Create a new **public** repo on GitHub.
2. Upload `index.html` (and this `README.md`) to the repo.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, set branch to `main` and folder to `/ (root)`, then save.
5. Wait about a minute — your site will be live at:
   `https://<your-username>.github.io/<repo-name>/`

## Customizing

- **Idea list**: edit the `ideas` array near the top of the `<script>` tag in `index.html`. Each idea has a `t` (text) and a `w` (weirdness, 1–5) — weirder ideas are `5`, tamer ones are `1`.
- **Attempts per slot**: change `MAX_ATTEMPTS_PER_SLOT`.
- **Timer length**: change `TIMER_SECONDS`.
- **Slot times**: edit the `currentSlotKey()` function and the `SLOT_WINDOWS` labels.

## Notes

- Since state is saved per browser, opening the site on a different device or browser starts a fresh streak there — it isn't synced across devices.
- This is a static, single-file app: no server, no database, no accounts.
