<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-review/commit/2e0f04a270e7cb39bc749bbfe3c405234a3babf9">2e0f04a</a>: fix: correct mate score sign in README example and fix misleading test comment

- README code snippet: negative MateIn values now render as -M<N> (e.g. -M2)
  instead of M-2, consistent with the CLI formatMateIn convention
- TestReviewer_ReviewGame_MultiPV: replace incorrect 'off-book' comment; the
  FEN used is the standard starting position so detectOpenings fires; the test
  focuses on MultiPV ordering and scores, not book detection
- <a href="https://github.com/ksysoev/chess-review/commit/50a3c069ff3212670274ffa2b5a3e6a730b4b009">50a3c06</a>: fix: restore field docs, remove dead hasExact field, enforce PV1 presence

- Restore all field-level GoDoc comments on MoveEvaluation and MoveReview
  that were stripped during fieldalignment reordering; documents sign
  conventions for MateIn/ScoreAfter, frame semantics for TopMoves, and
  other non-obvious API contract details.
- Remove unused hasExact bool from unexported pvEntry struct; the pvExact
  map's key presence already encodes exactness, the field was dead code.
- After building the result slice in analyzePosition, explicitly check that
  PV1 was observed and return ErrEngineFailure when it is absent; prevents
  reviewFromGameInfo from silently treating PV2 as the best continuation.
- <a href="https://github.com/ksysoev/chess-review/commit/ae79c8553a244d727b7edfff8e9711aa2eac86c2">ae79c85</a>: fix: address review comments on MultiPV top-moves feature

- review.go: derive maxPV from the maximum observed key in pvAny rather
  than len(pvAny), so sparse MultiPV indexes (e.g. PV1 and PV3 with no
  PV2) no longer silently drop higher-index PVs; cap at cfg.topMoves to
  discard unexpected extra PVs from the engine
- cmd/chess-review/main.go: truncate the Top Moves string to colTopMoves
  characters before passing to fmt.Fprintf so the fixed-width table
  column does not overflow when --top-moves is large
- README.md: expand the usage code snippet to format and print TopMoves
  inline, making it consistent with the example output block


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>