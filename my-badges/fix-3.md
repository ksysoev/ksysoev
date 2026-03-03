<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/47e8032d91df982ee73dca4ef47eea20f98a1dfb">47e8032</a>: fix: strip fragment and query from image refs before filesystem lookup in CollectAssets

A ref like "sprite.svg#icon" or "img.png?raw=1" was being used verbatim
for path resolution and os.ReadFile, causing the asset to be silently
skipped when no file with that literal name exists on disk. Parse each
ref with url.Parse and use only the path component, matching how
RewriteImageURLs rewrites the URL on the serve side.
- <a href="https://github.com/ksysoev/omnidex/commit/2216a3d4e1684c68b198090b10c97a34668a8d8a">2216a3d</a>: fix: address final PR review comments on asset support

- Preserve query string and fragment in RewriteImageURLs: parse src with
  url.Parse and rewrite only the path component, re-attaching RawQuery
  and Fragment afterward so references like sprite.svg#icon and
  img.png?raw=1 keep their semantics and already-encoded sequences are
  not double-encoded
- Add validateAssetRelPath guard to SaveAsset/GetAsset/DeleteAsset so
  paths like ../docs/readme.md are rejected even though they resolve to
  a location still within basePath (closes the assets-dir escape gap)
- Add configurable ingest body size limit: MaxIngestBodyMiB field in
  api.Config (default 50 MiB, overridable via API_MAX_INGEST_BODY_MIB);
  ingestDocs wraps r.Body with http.MaxBytesReader and returns 413 when
  the limit is exceeded
- Add/update tests for all three fixes
- <a href="https://github.com/ksysoev/omnidex/commit/76e7776ca790108581710847423d513bb469a0c4">76e7776</a>: fix: reject malformed percent-escape sequences in RewriteImageURLs


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>