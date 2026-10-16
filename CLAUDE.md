# Bouncy Ball

A launch-and-bounce physics puzzle game with a level editor. Tim's personal hobby game. There are no accounts, no backend and no multiplayer: each browser keeps its own levels in `localStorage`.

- **Live:** https://timothyhadfield.github.io/bouncy-ball/ (`index.html` redirects to `bouncy_game.html`)
- **Repo:** `TimothyHadfield/bouncy-ball` (public), branch `main`. GitHub Pages serves `main` from the root, with no build step.
- **Main checkout:** `OneDrive\Desktop\my-website\Code Projects\Games\Bouncy_ball`
- Handoff state is in `progress.md`.

## Files
- `bouncy_game.html`: the whole game in one file (inline CSS, plus about 2,100 lines of plain JS and Canvas 2D). Its sections are marked with `// ====` banners:
  - object classes: `GameObject`, `Ball` (physics, collisions), `Trampoline`, `Spike`, `Cup`, `Fan`, `Circle`, `Rectangle`, `Wall`
  - `Level` (`toJSON`/`fromJSON`), init/storage, menu, screens, settings, event listeners (game and editor mouse handlers), and the game loop / rendering
- `index.html`: a redirect shim only
- `README.md` and `docs/screenshots/*.png`: the GitHub showcase page

## How it works (facts that matter when editing)
- **World coordinates are fixed.** The floor is at `FLOOR_Y = 550`, and there are no side walls. The game and the editor each have their own camera (`cameraX/Y/Zoom`, `editorCameraX/Y/Zoom`). Convert screen to world with `(pos - camera) / zoom`.
- **Physics runs once per animation frame** (no fixed timestep), so game speed follows the display's frame rate. The ball's speed is capped at 22 and split into sub-steps of 2 px or less to stop it passing through things.
- **Each level has its own physics settings:** `gravity`, `bounciness` and `friction`. The Settings sliders write to the current level and save straight away.
- **Storage key `bouncyBallLevels`** holds a JSON array of `Level.toJSON()`. If the saved data can't be read, the raw text is copied to `bouncyBallLevels_backup` before the default "Tutorial" level replaces it. If storage is blocked, the game still runs but nothing persists.
- **Editor edits change the level object in place.** They reach storage only through Save, Play Level, or a Settings change (any of these saves every level).
- **Win:** the ball sits slow inside the cup for more than 30 cup checks. **Spike:** a tip hit kills the ball, and `Ball.die()` respawns it after 1 s. `reset()` cancels that timer.
- **Input is mouse only:** left-drag aims and launches, right-drag pans, the wheel zooms (in the editor it resizes the selected piece), and Delete/Backspace removes a piece. There are no touch handlers, so it is laptop-first (see Traps).

## Run locally
```
python -m http.server 8101     # from this folder, run in the background
```
Then open http://localhost:8101/.

## Test
There is no test suite and no framework. Don't add one unless Tim asks. Verify with phone-view:
- `node ~/.claude/tools/phone-view.mjs http://localhost:8101/ --desktop --eval "<js>"`. The game's globals (`levels`, `startLevel`, `editLevel`, `ball`, `currentLevel`, `getResizeHandles` ...) are reachable from `--eval`. Return a Promise to wait.
- **Headless WebKit runs requestAnimationFrame at about 12 fps.** Allow several seconds for anything frame-counted (the win needs 30+ frames).
- **Drag flows:** dispatch `MouseEvent`s on `editorCanvas` / `gameCanvas` with `clientX/Y` (`--do` can only click).

## Deploy
Push to `main`. Pages rebuilds within about a minute. Check it with `python ~/.claude/hooks/live-check.py "<main checkout>"`.

## Traps
- **The phone doesn't work as a game:** a tap gives zero launch power, the editor can't drag, and at 393 px the editor toolbar (about 570 px wide) overflows and covers Menu / Play Level / Save. The README says "best on a laptop". Touch support or a phone layout is **Tim's call** (a feature and a visual change), so don't add it uninvited.
- The menu's edit (pencil) and delete (x) buttons only appear on `:hover`.
- **Menu thumbnails scale by the current window size,** so a level built on a wide screen looks cropped on a narrow one.
- **Canvases are not scaled for devicePixelRatio,** so drawing is soft on retina screens. Changing that changes how the game looks, so it is Tim's call.
- **`getRotationHandlePos()` is unused.** The rotation handle math lives inline in `onEditorMouseDown` and `renderEditor`. Change both together.

## Standing instructions
No project-specific words from Tim are on record yet. The global rules in `~/.claude/CLAUDE.md` apply.
