<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-review/commit/40eda890d5a928d9247f4b89cb2588d9def7ebd5">40eda89</a>: fix: address remaining PR review concerns

- Define numPhases const derived from Endgame iota to replace hardcoded
  [3] array sizes in PlayerSummary, Summarize, and buildPlayerSummary
- Add TestReviewer_AnalyzePosition_PrefersExactOverBound to verify that
  analyzePosition selects the last exact score over bound scores
- Add TestReviewer_ReviewGameFull_PlayerNames and
  TestReviewer_ReviewGameFull_ReviewsMatchReviewGame to cover the new
  public ReviewGameFull API
- <a href="https://github.com/ksysoev/chess-review/commit/8e09daf0a5f97bf2c0e8511ead32bc02f8e3cca9">8e09daf</a>: fix: address PR review concerns in summary.go

- Derive numClassifications from int(Brilliant)+1 to prevent drift with
  Classification iota constants
- Add lower-bound guard (>= 0) to Classification index check to prevent
  panic on negative values
- Replace if/else color dispatch with switch; unknown colors are skipped
  via continue instead of silently skewing black's stats
- Rewrite cpLoss doc comment to accurately describe both behaviors:
  improvements clamped to 0, large losses returned as -1 to signal skip
- <a href="https://github.com/ksysoev/chess-review/commit/f37f7b057ce3d166b3bffe8a7004970df3c1db2c">f37f7b0</a>: fix: make engine evaluation deterministic across runs

Use Stockfish's default of 1 thread instead of runtime.NumCPU() in the
CLI. Stockfish's Lazy SMP parallel search is not bit-reproducible with
multiple threads, causing accuracy and game rating to vary between runs
at the same depth.

Also prefer exact-bound scores over lowerbound/upperbound scores when
reading engine info lines, avoiding imprecise bound values leaking into
centipawn-loss calculations.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>