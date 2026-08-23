<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/mimir/commit/d751e5416dd3523f139f71b8a45ff25c37c8e240">d751e54</a>: fix: add blank line before if to satisfy wsl_v5 linter
- <a href="https://github.com/ksysoev/mimir/commit/877b2cb45afb16f064fe0ee7f245d295a7c4e43e">877b2cb</a>: fix: address PR review comments

- patchKey: add early Content-Type header check before io.ReadAll to
  avoid buffering large bodies that will be rejected with 415; core
  still owns the authoritative validation for non-HTTP callers
- parseIfVersion: reject ifVersion=0 with 400; valid stored versions
  start at 1 so 0 is ambiguous with the absent-parameter convention
- add TestAPI_putKey_ZeroIfVersion_Returns400 and
  TestAPI_patchKey_ZeroIfVersion_Returns400 to cover the new guard
- <a href="https://github.com/ksysoev/mimir/commit/5bcd2b0863710007ecfb0fc7b013c49c5a9da0a6">5bcd2b0</a>: fix: remove trailing newline in store.go to satisfy gofmt


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>