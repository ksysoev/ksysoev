<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-openings/commit/2a2ac25d31632c481124eac078fcb716c12d33f4">2a2ac25</a>: Fix PGN parsing for compact formats and add tests for LookupMoves/SearchMoves

Address PR review feedback: fix parsePGNMoves to strip move-number
prefixes instead of dropping entire tokens, which broke compact PGN
formats like '1.e4' and '1...e5'. Add missing test coverage for the
LookupMoves and SearchMoves public APIs.
- <a href="https://github.com/ksysoev/chess-openings/commit/fa53917dc76b12b9750dfc07a2cb519782e654ec">fa53917</a>: Fix misleading docstrings for parseOpenings and addEntry


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>