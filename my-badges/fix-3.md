<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/2c863f4d2516f253241a80b71135e441dd6451ed">2c863f4</a>: fix: remove ErrNotFound alias, validate repo param, use RFC3339Nano for UpdatedAt

- Remove redundant s3store.ErrNotFound alias; use core.ErrNotFound directly
  in Get and GetAsset to keep error sentinels centralized in pkg/core
- Add validateRelPath(repo) to all public Store methods (Save, Get, Delete,
  SaveAsset, GetAsset, DeleteAsset, ListAssets) to reject traversal attempts
  like "../other" with core.ErrInvalidPath, matching local docstore behaviour
- Switch UpdatedAt serialization from RFC3339 to RFC3339Nano to preserve
  sub-second precision; parseUpdatedAt helper accepts both formats for
  backward compatibility with existing objects
- Update tests: replace Truncate(time.Second) with Truncate(time.Nanosecond);
  add TestStore_InvalidRepoRejectsTraversal covering all 8 public methods
- <a href="https://github.com/ksysoev/omnidex/commit/56c6e7f66cb14aa1ae97f449cf3aa3735122851e">56c6e7f</a>: fix: address PR review comments on S3 document store

- Move ErrNotFound and ErrInvalidPath sentinel errors to pkg/core so both
  store backends and API handlers share the same values; fixes 404→500
  regression when using the S3 backend
- Move s3store.Config ownership to pkg/repo/s3store and add mapstructure
  tags; remove duplicate S3Config from pkg/cmd
- Add validateRelPath to s3store rejecting empty, absolute and traversal
  paths (mirrors docstore behaviour, returns core.ErrInvalidPath)
- Return error from Save when updateRepoMeta fails to keep repos discoverable
- Fall back to LastModified in Get/List when updated-at header is absent
- Replace full-bucket scan in ListRepos with two-level delimiter-based
  prefix enumeration for O(repos) rather than O(objects) scalability
- Reset docCount=0 on countDocs error to match log message
- Make unknown Storage.Type a hard startup error instead of silently
  falling back to local disk
- Fix MinIO healthcheck to use HTTP readiness endpoint instead of mc
- Run go mod tidy to promote direct AWS SDK imports from indirect
- <a href="https://github.com/ksysoev/omnidex/commit/7640f0cb87c4102b205fc9a9ce20ae992e686919">7640f0c</a>: fix: run go mod tidy to add missing go.sum entries for transitive deps


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>