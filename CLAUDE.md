# Midnight at Mustang Memorial

Single-file web game (index.html) for Human A&P: a cell structure/function escape room.
Plain HTML/CSS/JS, no framework, no build step. Deployed on Vercel from GitHub.

## Structure (all inside index.html)
- Content pools: STRUCT, RIDDLES, MATCHP, ORDERS, CONNS, FMPOOL, L3MC, SORTCATS, BUILDS, CASES
- buildGame(seed, caseId) assembles each student's randomized game from those pools
- Proficiency: profOf(hints) → 6+ hints = Level 1, 4–5 = Level 2, 0–3 = Level 3
- Midnight cap: after 60 min of active time (activeMs), levelFor() caps the level at 2 unless extended time (PREFS.ext, recorded per attempt as S.extUsed) was on
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
- Keep all code in the single index.html file. The only other asset is mustang.png (the school logo), which must stay committed alongside it.
- Organelle mini-icons on answer options appear only in Level 2 (Old Apothecary) and Room 13. Never show them in Level 1 or Level 3, because they make identification too easy.
- After any change, check that the page loads without console errors.
- Show me the planned change before editing, and keep student-facing text
  warm, clear, and appropriate for high school A&P students.
