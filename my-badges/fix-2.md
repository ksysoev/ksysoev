<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/ffdf1954f8edcacf79c7300792f1d4daf4997129">ffdf195</a>: fix: address remaining PR review comments on asset support

- Change Assets field to *[]IngestAsset so server can distinguish nil
  (absent field, older client) from an explicit empty list (new client
  requesting stale-asset cleanup); update sync guard to req.Assets != nil
- Fix directory traversal check to use == ".." || HasPrefix("../")
  instead of HasPrefix("..") which falsely blocked paths like ..images/
- URL-encode asset path segments in RewriteImageURLs via url.JoinPath to
  produce valid URLs for paths containing spaces, #, ? etc.
- Rename ErrNotFound message to "not found" to cover both documents and assets
- Add tests for nil-vs-empty Assets sync, ..foo path, and URL encoding
- <a href="https://github.com/ksysoev/omnidex/commit/99eb8712a8f6fc4d82c1e4928ff677ae0c1c2eb0">99eb871</a>: fix: address PR review comments on asset support

- Guard syncDeleteStaleAssets behind len(req.Assets) > 0 to prevent
  older clients (omitting the assets field on sync) from wiping all
  stored assets for a repo
- Handle docstore.ErrInvalidPath in assetPage as 400 Bad Request
  instead of 500, with no server-error log entry
- Add X-Content-Type-Options: nosniff and Content-Security-Policy:
  sandbox headers to asset responses to mitigate SVG XSS
- Validate non-empty Path and Content in upsertAsset before decoding
- Update and extend tests: sync-no-assets guard, empty asset fields,
  security headers, ErrInvalidPath handler behaviour


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>