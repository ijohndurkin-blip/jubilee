# The Jubilee: Last Orders

A 3D pub reaction game. Customers walk up to the bar of The Jubilee (est. 1887). Read what they say, watch them closely, and decide in seconds:

- **Good** → **SERVE** them a pint
- **Evil** → **SHOOT**

Type your name, pick **Barmaid** or **Barman**, and open the bar. Your name stays at the top of the screen while you play. A wrong call or being too slow gets you shot. You have 2 lives, and 10 in a row wins one back.

## Features

- **Player names + global leaderboard.** Every player enters a name before playing. The **Hall of Fame** (top 20 games — a player can appear more than once) shows on the start screen and again at closing time. Every finished shift is saved for good. Scores made offline are queued and sent the next time you play.
- **Full screen.** Use the ⛶ button (or press **F**). On iPhone, tap Share → *Add to Home Screen* and open it from there to play full screen.
- **Sneakier every round.** From round 2 on, villains hide their tells: less coats and shifty looks, more smiles, friendly small talk, quicker and dimmer red eye glints. Meanwhile the regulars look shiftier, say alarming things, and their glasses catch the light. Only the red flash in the eyes never lies.
- **Shotgun streaks.** Get **5 right in a row** and you're handed a shotgun. It stays loaded until the next villain walks in: hit **BLAST** and they get blown in slow motion clean out of the front door, for double points + 250. A wrong call drops it.
- **Better graphics.** Bloom lighting, reflections on brass and glass, a filmic grade, rain on the windows, a live fire with embers, dust in the lamplight, contact shadows and more detailed characters. It steps quality down automatically on slower phones.

## Controls

| Action | Touch | Keyboard |
| --- | --- | --- |
| Serve | SERVE button | ← or A |
| Shoot / Blast | SHOOT button | → or D or Space |
| Full screen | ⛶ | F |

## Running it

It's a static site, so no build is needed. Serve the folder with any web server, for example:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. It's deployed with GitHub Pages straight from this repo.

## Leaderboard backend

Scores live in a Supabase Postgres table, `public.jubilee_scores`. The browser can't touch that table directly. It can only call two database functions through the public (publishable) API key:

- `jubilee_submit(name, score, correct, best_streak, round)`: checks the name (1 to 18 characters), checks the score is plausible for the number of correct calls, and rate-limits each name
- `jubilee_top(limit)`: returns each player's best shift, highest first

Three.js r160 and its post-processing add-ons are bundled under `vendor/` (MIT licence, see `vendor/THREE-LICENSE`).
