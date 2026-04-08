<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-review/commit/1a95bc71b38c1d575a5e387e2488d82c81023d2f">1a95bc7</a>: fix: guard analyzePosition safety-net against non-terminal positions

Switch on positionStatus() result instead of treating any non-stalemate
bestmove=(none) as checkmate. The default branch now returns ErrEngineFailure
for FEN parse failures or other unexpected non-terminal statuses, preventing
them from being silently masked as a false checkmate evaluation.
- <a href="https://github.com/ksysoev/chess-review/commit/8e41fb8e60a821e675f2c11b03a830affd4aa6b6">8e41fb8</a>: fix: correctly represent stalemate as draw with nil MateIn

- positionStatus helper reconstructs position from FEN+UCI moves using the
  chess library to determine checkmate vs stalemate status
- reviewFromGameInfo: stalemate now sets MateIn=nil (draw) instead of &0
  (checkmate); fixes downstream M0 display for stalemate positions
- analyzePosition safety-net: uses positionStatus to distinguish stalemate
  (Score=0, MateIn=nil) from checkmate (Score=-mateScoreSentinel, MateIn=&0)
- Update stalemate test to assert MateInAfter is nil
- <a href="https://github.com/ksysoev/chess-review/commit/eb22010f963cb9021fd00fe03f6cc8064e5c5678">eb22010</a>: fix: handle terminal positions (checkmate/stalemate) in game review

When a game ends in checkmate or stalemate, Stockfish responds to the
post-move position analysis with 'bestmove (none)' and no evaluation
lines, causing analyzePosition to return ErrEngineFailure and abort
the entire game review.

Fix by propagating terminal-position state from parsePGN through
moveInfo.IsTerminal/IsStalemate into reviewFromGameInfo, which now
synthesises the post-move evaluation directly instead of calling
analyzePosition:
  - checkmate: Score=-mateScoreSentinel, MateIn=0
  - stalemate: Score=0 (draw), MateIn=0

Also add a safety-net guard in analyzePosition itself: when bestMove
is "(none)" and pvAny is empty, return the synthetic mate-0 evaluation
rather than ErrEngineFailure, protecting any direct callers.

Closes #22


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>