# Bouncy Ball: progress

## START HERE
Last updated 2026-10-16. Read in this order: `CLAUDE.md` (what the project is, the file map, how to test), then this file.

## Goal right now
None set. The game works on a laptop. The 2026-10-16 sweep fixed bugs only and changed nothing visible.

## Status
| Area | State |
|---|---|
| Play (laptop) | Works: launch, bounce, cup win, spike death and respawn |
| Level editor (laptop) | Works: place, move, resize, rotate, walls, save, per-level physics |
| Phone | Not playable (mouse-only input). Tim's call, see Traps |
| Hosting | GitHub Pages from `main`, https://timothyhadfield.github.io/bouncy-ball/ |
| Tests | No suite. Verified with phone-view `--eval` scripts |

## Authorized next steps
None.

## Standing instructions
- None recorded for this project yet. The global rules in `~/.claude/CLAUDE.md` apply.

## Traps
- The editor saves edits only on Save, Play Level or a Settings change. Leaving via Menu keeps them in memory until reload, then they are lost.
- Headless WebKit runs frames at about 12 fps, so wait long enough in phone-view checks.
- See `CLAUDE.md` Traps for the phone, hover-only and thumbnail issues.

## Decisions
- 2026-10-16 · Bug sweep:
  - The spike respawn timer is now cancelled by a reset.
  - Resize handles work on rotated pieces.
  - Blocked or full storage no longer crashes the menu.
  - Unreadable saved levels are copied to `bouncyBallLevels_backup` instead of being lost.
  - Nothing visible changed.

## NOT verified
- A real iPhone (only Safari's engine through phone-view).
- Behaviour at real 60/120 Hz: physics runs per frame, so speed depends on the screen's refresh rate.

## Rejected / parked
- (parked, Tim's call) Touch controls and a phone layout for the editor toolbar.
- (parked, Tim's call) Sharper rendering on retina screens (devicePixelRatio).
