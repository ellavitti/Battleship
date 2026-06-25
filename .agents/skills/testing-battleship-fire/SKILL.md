---
name: testing-battleship-fire
description: Test the Battleship fire/AI-targeting logic in battleship.html end-to-end. Use when verifying changes to firing, hit/sink detection, or the AI hunt/target state machine.
---

# Testing Battleship fire / AI-targeting logic

`battleship.html` is a single self-contained file (no build, no server, no CI).
Open it directly with `file:///path/to/battleship.html` in the browser.

## Key code map
- `aiTurn()` — AI hunt/target state machine: `huntMode`, `originHit`,
  `currentDirection`, `triedDirections`. Hunt = random fire; target = drill
  around a known hit.
- `checkSunk(ship, board)` — marks a ship sunk. Called from BOTH firing paths:
  player firing at the AI board AND the AI firing at the player board. Anything
  that resets shared state here is suspicious — it must be guarded by which board
  was hit (e.g. `if (board === playerBoard) resetAITargeting()`), otherwise a
  player action corrupts AI state (or vice-versa). This was the real bug fixed in PR #1.
- `resetAITargeting()` — clears the AI hunt/target state.

## Most valuable tests
1. **Cross-contamination**: the AI's hunt state must survive the *player* sinking
   an AI ship. This internal state is NOT visible in the stock UI.
2. Normal firing regression: shots register (hit=red, miss=gray), turns alternate,
   AI fires back, status text updates.

## How to test internal AI state (it is invisible in the stock UI)
The bug is in internal state, so screenshots of the normal board prove nothing.
Make TWO temporary copies in `/tmp` and inject a debug panel + scenario button:
- `/tmp/test_fixed.html` — current repo code.
- `/tmp/test_buggy.html` — the fix reverted, to prove the test actually detects the bug.
- Inject a debug panel that renders `huntMode`, `originHit`, `currentDirection`,
  `triedDirections` (re-render it after every click).
- Inject a "Setup Test Scenario" button that deterministically: starts a battle,
  forces the AI into target mode on a player cell (`huntMode=false`, set `originHit`),
  and marks all-but-one cell of an AI ship as hit so ONE click sinks it. Highlight
  the kill cell (e.g. yellow) so the click coordinate is obvious.
- Drive the scenario with REAL UI clicks on the kill cell (exercises
  `handlePlayerClick` -> `checkSunk(cell.ship, aiBoard)`), not console hacks.
- Run the identical scenario on both builds and diff the debug panel:
  buggy -> `huntMode` flips true / `originHit` null; fixed -> state preserved,
  and `triedDirections` updates (AI keeps hunting). Always run the buggy build too —
  a side-by-side divergence is the proof the test is meaningful.

## Static / fast verification (no browser)
A Node headless harness that stubs the DOM and runs ~2000 AI-only games is great
for catching double-fires, stuck/infinite turns, out-of-bounds shots, and runtime
errors. Keep it as `/tmp/harness.js`. It can't catch player-vs-AI cross-contamination,
so still do the browser test above for that class of bug.

## Gotchas
- Coordinates: identify the kill cell from the screenshot each run — random ship
  placement means the cell moves between runs.
- Recording: maximize the window first (`wmctrl -r :ACTIVE: -b add,maximized_vert,maximized_horz`).
- Cleanup: the debug panel / scenario button live ONLY in the `/tmp` copies — never
  commit them into `battleship.html`.

## Devin Secrets Needed
None. Fully local, no auth, no network.
