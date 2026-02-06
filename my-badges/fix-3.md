<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/make-it-public/commit/ea5e4e3fae92c37c7116eb57fb7a458367c3c6c2">ea5e4e3</a>: fix: address PR review - Unicode handling, cleanup, and documentation

Phase 3: Low priority robustness improvements
- Replace len() with utf8.RuneCountInString() in banner.go for correct Unicode padding
- Replace len() with utf8.RuneCountInString() in request.go for correct Unicode separator
- Add defer spinner.Stop() in client.go to ensure cleanup on unexpected exits
- Document global color state modification in display.go New() function
- Explain single-instance design assumption and potential refactoring path

Fixes Unicode text alignment issues and improves resource cleanup robustness
identified in PR #242 review comments.
- <a href="https://github.com/ksysoev/make-it-public/commit/b9817c1094cb4b8dc4af33a15085e8459a8c3b56">b9817c1</a>: fix: address PR review - prevent channel double-close and test state pollution

Phase 2: Medium priority concurrency safety fixes
- Add sync.Once to Spinner struct to prevent channel double-close panics
- Implement closeChannel() helper method using sync.Once.Do()
- Replace all direct close(s.done) calls with safe closeChannel() method
- Replace init() with TestMain() in display_test.go to properly restore color state
- Ensures test color state is saved and restored, preventing global pollution

Fixes race condition and test isolation issues identified in PR #242 review.
- <a href="https://github.com/ksysoev/make-it-public/commit/4c0c6497a344d5a5fcbf2c222fcc836974a07cd7">4c0c649</a>: fix: address PR review - add pipe error handling and resource cleanup in tests

Phase 1: High priority test quality fixes
- Add error checking for os.Pipe() calls in all test functions
- Add defer r.Close() to prevent pipe reader resource leaks
- Ensures proper resource cleanup in TestServeHTTP, TestPrintBody, TestPrintText,
  TestPrintJSON, and TestServeHTTPNonInteractive

Fixes resource leak issues identified in PR #242 review comments.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>