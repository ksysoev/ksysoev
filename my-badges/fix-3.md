<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/55905d07c65b9e51af5d0ac141f57a8cbabe5d0c">55905d0</a>: Fix syncDeleteStale dropping partial orphan-cleanup count on error
- <a href="https://github.com/ksysoev/omnidex/commit/fe3196514f8cafc1b8466d96c092abfe13044e31">fe31965</a>: Fix ListByRepo silent truncation and reduce sync log noise

Paginate ListByRepo to collect all results instead of silently
truncating at 10k documents, preventing orphan cleanup from missing
entries. Downgrade per-document sync/orphan removal logs from INFO
to DEBUG and add INFO-level summaries with counts.
- <a href="https://github.com/ksysoev/omnidex/commit/965b7c1a1a40c01f08b0c40f3c6334d74107f6e1">965b7c1</a>: Fix sync leaving orphaned documents in search index

Reverse the delete operation order in deleteDocument() to remove from
the search index before the docstore. This prevents permanent orphans
when the search removal fails after the docstore deletion succeeds,
making the operation self-healing via subsequent sync retries.

Add ListByRepo to the search engine interface so syncDeleteStale() can
also detect and clean up any existing orphaned search entries left by
prior partial failures.

Closes #29


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>