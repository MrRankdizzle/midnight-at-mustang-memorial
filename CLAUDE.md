# Midnight at Mustang Memorial

Single-file web game (index.html) for Human A&P: a cell structure/function escape room.
Plain HTML/CSS/JS, no framework, no build step. Deployed on Vercel from GitHub.

## Structure (all inside index.html)
- Content pools: STRUCT, RIDDLES, MATCHP, ORDERS, CONNS, FMPOOL, L3MC, SORTCATS, BUILDS, CASES
- buildGame(seed, caseId) assembles each student's randomized game from those pools
- Proficiency: profOf(hints) → 5+ hints = Level 1, 3–4 = Level 2, 0–2 = Level 3
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
- Keep the Carolina blue / sky blue / white palette and the existing fonts as defaults.
- Keep everything in the single index.html file.
- After any change, check that the page loads without console errors.
- Show me the planned change before editing, and keep student-facing text
  warm, clear, and appropriate for high school A&P students.
