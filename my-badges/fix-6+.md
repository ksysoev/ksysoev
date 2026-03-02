<img src="https://my-badges.github.io/my-badges/fix-6+.png" alt="I did 7 sequential fixes." title="I did 7 sequential fixes." width="128">
<strong>I did 7 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/4a71d7d3bc28613ab5d7fa5cca802e78203e8fe4">4a71d7d</a>: fix: align ToPlainText with ExtractHeadings for empty-name tags

ToPlainText was emitting a blank line for tags with an empty name while
ExtractHeadings already skipped them, causing byte-offset misalignment
during anchor resolution. Add the same tag.Name != "" guard to
ToPlainText and cover the invariant with a new test case.

Also update a stale Swagger UI reference in processor_test.go to Scalar
API Reference, and document the known slug de-duplication limitation in
the githubSlug comment.
- <a href="https://github.com/ksysoev/omnidex/commit/9784c4fc4ed35870b9aa9f9c8c41ef493ed2862a">9784c4f</a>: fix: address PR review comments — UTF-8 rune boundary and test subtest names
- <a href="https://github.com/ksysoev/omnidex/commit/5cba28e991341a24aa7f19874ab6eed0e450bf13">5cba28e</a>: fix: address PR review comments — rune-safe caseInsensitiveIndex and whole-line heading matching

- caseInsensitiveIndex: replace byte-length window with rune-count sliding
  window so s[windowStart:windowEnd] is never split mid-rune for multi-byte
  Unicode characters (Copilot comment #9)
- findAnchorAtPosition: introduce findHeadingLine helper that requires a
  whole-line match (preceded/followed by newline or string boundary) to
  avoid attributing incorrect anchors when heading text also appears in
  body paragraphs (Copilot comment #10)
- Update stale parseSpec comment: Swagger UI -> Scalar API Reference (#2)
- Update len(headings)==0 comment to reflect both no-headings and
  no-heading-support cases (#8)
- Add TestFindHeadingLine, TestCaseInsensitiveIndex, and a false-positive
  body-match case to TestFindAnchorAtPosition
- <a href="https://github.com/ksysoev/omnidex/commit/d61d994a71fb5c179b711e800549e3ca7f74bc42">d61d994</a>: fix: address remaining PR review comments on granular search anchors

- Remove stale '(e.g. OpenAPI)' from heading navigation comment in svc.go;
  OpenAPI now has a full ExtractHeadings implementation
- Rename TestGithubSlug to TestGitHubSlug for correct capitalization
- Replace per-call regexp.Compile in caseInsensitiveIndex with a
  strings.EqualFold sliding-window scan (utf8.DecodeRuneInString advance),
  eliminating per-call allocation while keeping correct Unicode byte offsets
- <a href="https://github.com/ksysoev/omnidex/commit/c03e6772f19730a409e72fd2ac24b93e80e3567a">c03e677</a>: fix: address PR review comments on granular search anchors

- Extract scrollToHash() from initScrollSpy() so hash-based scroll
  always runs on htmx:afterSwap regardless of TOC sidebar presence
- Replace caseInsensitive string index using strings.ToLower with
  caseInsensitiveIndex() backed by regexp to avoid Unicode byte-offset
  mismatches (e.g. Turkish dotless-i, German eszett)
- Remove dead findAnchorForFragment; rewrite its tests against the
  production findAnchorAtPosition function directly
- Update stale Swagger UI references to Scalar API Reference in
  pkg/prov/openapi/processor.go comments
- <a href="https://github.com/ksysoev/omnidex/commit/4caf622d58a307ec1697688103dd133ecd5943d5">4caf622</a>: fix: correct fragmentMatchIndex ellipsis/partial-word handling and test expectations

skipPartialLeadingWord now only strips the leading segment when the first
character is a lowercase ASCII letter (the tell-tale of a Bleve mid-word cut
after '…'). It also advances to the first newline rather than the first space
so that a partial trailing line like 'ome content.\nSetup\n' is consumed as a
unit, ensuring the no-mark fallback path resolves to the correct section.

The wantIdx for the 'bleve ellipsis, mark in usage section' test case was
wrong (219); 'using' is at byte offset 175 in the test's plainText fixture,
which is what the implementation correctly returns.
- <a href="https://github.com/ksysoev/omnidex/commit/6373d1ddbf5acb7c3cd963a0411cb5922903fad7">6373d1d</a>: fix: resolve build failure and lint issues in granular search anchor implementation

- Fix fieldalignment-broken positional struct literals in collectMethodOperations
  by converting candidate struct to named-field literals and reordering fields
- Fix wsl_v5: add missing blank lines in githubSlug function body
- Fix staticcheck S1016: use methodOperation(c) type conversion instead of
  field-by-field struct copy in collectMethodOperations
- All tests pass and golangci-lint reports 0 issues


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>