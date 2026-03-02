<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/aa8581b6472827164d9a0e52f9057376f59b4199">aa8581b</a>: fix: percent-encode path segments in githubBlobURL and add test coverage

- Use url.PathEscape on each path segment to handle spaces, '#', '?', and
  other reserved characters that would produce malformed GitHub blob URLs
- Add TestGithubBlobURL table-driven unit tests covering SHA present,
  empty SHA fallback to main, and paths with special characters
- Add View source URL assertions to TestRenderDoc_FullPage and
  TestRenderDoc_OpenAPI_FullPage
- Add TestRenderDoc_ViewSourceLink covering both CommitSHA and main fallback
  scenarios through the full template rendering pipeline
- <a href="https://github.com/ksysoev/omnidex/commit/510143894771a25f22cce0172ca0e27100743484">5101438</a>: fix: fix seed paths to match actual repo layout for valid View source links

The seed container was mounting only ./docs/sample as /docs, so documents
were indexed with bare filenames (e.g. getting-started.md). The View source
links therefore pointed to non-existent paths on GitHub.

Mount the repo root as /repo and scope the file pattern to
docs/sample/**/* so stored paths become docs/sample/getting-started.md
etc., matching their real location in the repository. Also correct the
repo identifier to ksysoev/omnidex and set commit-sha to main so
generated GitHub links resolve immediately.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>