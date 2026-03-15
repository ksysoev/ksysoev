<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-review/commit/3d31c028f7a47fa4da884332efba6205d0522e68">3d31c02</a>: fix: address second-round PR review comments

- Add Cause error field and Unwrap() to ErrInvalidPGN and ErrEngineFailure so
  callers can use errors.Is/As on the root cause; propagate originating errors
  at all construction sites in review.go and pgn.go
- Validate option values in New(): return an error for depth/threads/hashMB < 1
  to prevent silent invalid engine configuration
- Guard Reviewer zero value: add doc comment and nil checks in ReviewGame/Close
  that return ErrEngineFailure instead of panicking
- Add TestMoveToUCI_Promotion and TestMoveToUCI_Castling to cover the promotion
  suffix (e7e8q) and castling (e1g1) paths in moveToUCI
- Add TestNew_InvalidOptions covering all six zero/negative option combinations
- Add TestReviewer_ZeroValue_ReviewGame/Close for the nil-engine guard
- Update package doc to enumerate all seven classification types including Miss
- <a href="https://github.com/ksysoev/chess-review/commit/4b1f78ed2a315b4c85083453d32fd32acb53ec29">4b1f78e</a>: fix: address PR review comments on correctness, performance, and docs

- Handle mate scores in analyzePosition: map mate-in-N to ±30000
  sentinel via normalizeScore so downstream arithmetic stays valid
- Return ErrEngineFailure when engine stream closes without a bestmove
  event instead of silently returning zero values
- Halve engine calls in ReviewGame from 2N to N+1 by carrying the
  score forward between plies
- Add Miss classification for moves that throw away a forced mate
  (sentinel loss ≥ 20000 cp)
- Fix off-by-one in Excellent comment: 1–10 cp → 0–10 cp
- Remove stale sentence from parsePGN doc comment
- Add tests for mate score, no-best-move, and normalizeScore


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>