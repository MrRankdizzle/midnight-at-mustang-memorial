# Midnight at Mustang Memorial

Single-file web game (index.html) for Human A&P: a cell structure/function escape room.
Plain HTML/CSS/JS, no framework, no build step. Deployed on Vercel from GitHub.

## Structure (all inside index.html)
- Content pools: STRUCT, RIDDLES, MATCHP, ORDERS, CONNS, FMPOOL, L3MC, SORTCATS, BUILDS, CASES
- buildGame(seed, caseId) assembles each student's randomized game from those pools
- Proficiency: levelFor() = the lowest of three limits (accuracy, hints, midnight cap). Level 0 is NE (Not Enough Evidence), below Level 1; show it as "NE", never "Level 0" (lvName/lvFull).
  - Accuracy: first-try correct answers / total answers. 80%+ = Level 3, 60–79.99% = Level 2, 40–59.99% = Level 1, under 40% = NE. Compared in whole numbers (10c >= 8n) so exactly 80% is Level 3. No answers yet = not limiting.
  - Answers per challenge (stepsOf): mc, tap, unscramble = 1. Label = 1 per pin, match = 1 per pair, order = 1 per step, sort = 1 per cell, fact or myth = 1 per statement, build = 1 per row (judged on the first "Test my cell" only). Connections = its 3 groups, always counted correct (trial and error is the point).
  - Tracking: S.cur.wm marks missed steps and wmc counts misses charged to steps. solve() stores {m, h, n, c} in S.rec. Records without n/c (older saves) are estimated by recScore as max(0, steps - misses). Misses and hints on an unsolved challenge are kept in S.pend, so leaving and coming back can't reset them.
  - Hints: profOf(hints) → 6+ hints = Level 1, 4–5 = Level 2, 0–3 = Level 3.
  - Midnight cap: after 60 min of active time (activeMs), the level is capped at 2 unless extended time (PREFS.ext, recorded per attempt as S.extUsed) was on. Turning the time limit off removes only this cap.
  - setBy() names the limit or limits that set the final level, for the poster and the top-bar tooltip.
- Icons are inline SVG in ICONS; no emoji anywhere in the UI
- Sounds are synthesized with Web Audio in SFX; no audio files
- Accessibility settings (font, text size, sound) are stored separately from game progress

## Rules
- Do not rename the localStorage keys "mustang-memorial-escape-v4" or
  "mustang-memorial-prefs". Renaming them erases every student's saved progress.
- Students' games are rebuilt from a saved seed. Changing the order or contents
  of existing content pools changes questions for students mid-game. Prefer
  appending new items to the end of pools, and make bigger content changes
  between units.
- Generator versioning: each game saves the version of buildGame's selection
  logic it was built with (S.gv, set from GEN_VERSION in startGame). Saves
  without gv are version 1. When a change would alter how buildGame picks or
  orders questions, bump GEN_VERSION and put the new logic behind
  `gv >= N`, leaving the older branches untouched so in-progress games keep
  their questions. Version 2 picks the Level 1 unscramble word from UNSCR and
  keeps it out of the other Level 1 challenges.
- Keep the Carolina blue / sky blue / white palette and the existing fonts as defaults.
- Keep all code in the single index.html file. The only other asset is mustang.png (the school logo), which must stay committed alongside it.
- Organelle mini-icons on answer options appear only in Level 2 (Old Apothecary) and Room 13. Never show them in Level 1 or Level 3, because they make identification too easy.
- After any change, check that the page loads without console errors.
- Show me the planned change before editing, and keep student-facing text
  warm, clear, and appropriate for high school A&P students.
