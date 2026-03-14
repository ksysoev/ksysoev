<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/stockfish/commit/ffb48e209372baf77e143ececde01b2a8ac9eb6c">ffb48e2</a>: fix: prevent runSearch deadlock when caller stops reading the result channel

Replace blocking channel sends in runSearch with select statements that
select on ctx.Done(), so a slow or non-reading caller cannot stall the
engine read loop or prevent searchState.finish() from running.

- bestmove send: best-effort delivery via select; return is unconditional
  so the deferred finish() always fires regardless of whether the send
  succeeded
- info sends: exit runSearch on ctx.Done() instead of blocking, keeping
  the lineCh consumer unblocked

Add TestClient_Go_SlowConsumer and TestClient_Go_FullBuffer to reproduce
both deadlock scenarios (>32 info lines without reading, and exactly full
buffer before bestmove).
- <a href="https://github.com/ksysoev/stockfish/commit/4bf77a80969c8d25da9d193f3d1e0701e92a506c">4bf77a8</a>: fix: address PR review comments on guards and drain robustness

- Add ErrEngineNotRunning guard to all public methods (IsReady, NewGame,
  SetOption, SetPosition, Go, Bench, Eval, Display, Flip, Compiler,
  ExportNet) so calls after Close return a clear error instead of writing
  to a closed stdin
- Add ErrSearchInProgress guard to Flip and ExportNet to prevent sending
  non-search commands while runSearch is consuming lineCh
- Fix drainDiscardUntilBestMove to select on eng.done in addition to
  lineCh, preventing an indefinite goroutine hang when the engine crashes
  without emitting bestmove
- Clarify Go() docstring: on cancellation bestmove is drained internally
  and the channel closes without a final bestmove entry
- Add 17 new tests covering the above guards


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>