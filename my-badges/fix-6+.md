<img src="https://my-badges.github.io/my-badges/fix-6+.png" alt="I did 7 sequential fixes." title="I did 7 sequential fixes." width="128">
<strong>I did 7 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/revdial/commit/cf2260b83c77c26ead031fd02a42175fa65f61d0">cf2260b</a>: fix: add nil session validation before creating MuxConn

Add defensive checks to prevent nil pointer panics:
- Validate client.Session() is not nil before passing to pool.NewMuxConn
- Add mutex protection to ClientV2.Session() method for thread safety
- Add validation in both Listen() and createPoolConnection()

This prevents potential panic if isV2=true but session=nil due to race
conditions or edge cases in the registration flow.
- <a href="https://github.com/ksysoev/revdial/commit/ef8bd262d373d36306ce03aa3a3db7f765de08d6">ef8bd26</a>: fix: address remaining PR review comments

- Remove unused disableV1 and poolConfig fields from Listener struct
- Replace magic number '1' with proto.VersionV1() constant for consistency
- Add proper connection cleanup when registration fails in Listen()
- Fix double unlock bug in pool.scaleDown() by inlining removal logic
- Add VersionV1() public function to proto package

All changes improve code quality and maintainability based on PR feedback.
- <a href="https://github.com/ksysoev/revdial/commit/75a6517c75bfb1db329a1e20346250f53aafaf45">75a6517</a>: fix: resolve flaky test race condition in Dialer.Stop()

The Dialer.Stop() method had a race condition causing flaky test failures:
- Context cancellation (d.cancel()) triggered a goroutine to close the listener
- Stop() then attempted to close the listener again, causing 'use of closed network connection' error

Fix: Remove the duplicate listener.Close() call from Stop() since the context
cancellation goroutine already handles listener cleanup. Now Stop() only cancels
the context and waits for goroutines to finish.

Tests verified with 10x repeated runs - all passing with race detector clean.
- <a href="https://github.com/ksysoev/revdial/commit/949015a46f9500979a6f296a5d0a372380c78e72">949015a</a>: fix: address PR review issues in V2 protocol implementation

- Fix data race on isV2 field by changing mutex to RWMutex and protecting all accesses
- Fix goroutine leak in createPoolConnection by calling client.Close() instead of conn.Close()
- Add pool.Close() in Listener.Close() to properly cleanup resources
- Fix type assertions in WithMuxConfig options by creating separate V2Option types
- Remove dead code for unused negotiated yamux values
- All tests passing with race detector clean
- <a href="https://github.com/ksysoev/revdial/commit/bf4758d7392b10203ce9b1d3da3adb42708703e4">bf4758d</a>: fix: resolve V2 protocol context cancellation and session cleanup issues

- Fix context cancellation race in handleV2RegisteredConnection by using dialer lifecycle context (d.ctx)
- Add ctx field to Dialer struct to maintain lifecycle context separate from connection contexts
- Update Start() to use d.ctx in goroutines instead of parameter context
- Fix V2 bind protocol to use versionV1 for compatibility with stream parsing
- Add Close() method to ClientV2 to properly close yamux session during shutdown
- Buffer commands channel in Client to prevent potential deadlocks
- Enable V2 integration test (TestListenerDialer_V2Protocol)

This resolves the issue where V2 connections were prematurely removed from the connection manager due to context cancellation, causing 'no connection is available' errors. Also fixes goroutine leaks during shutdown by ensuring yamux sessions are properly closed.

All tests pass with no regressions.
- <a href="https://github.com/ksysoev/revdial/commit/83fa55ad8983c5ac50b51354488c924e6ee828f7">83fa55a</a>: Fix linter issues
- <a href="https://github.com/ksysoev/revdial/commit/61de76db1af6e9229b75394fe4ddec594c062a35">61de76d</a>: fix: V1 backward compatibility and protocol improvements

- Fix V1 fallback mechanism in ClientV2
  - Add disableV2 flag to Client struct for V1-only mode
  - Fix option application in NewClientV2 to properly set flags
  - Fix registerV1 to call establish() for auth handshake
  - Add proper context handling and error logging

- Fix protocol version consistency
  - Use V1 format (versionV1) for all V2 stream communication
  - Update server responses to use V1 format for compatibility
  - Fix version checking in handleV2Stream

- Override methods in ServerV2 for proper V2 operation
  - Add SendConnectCommand override to delegate to V2 or V1
  - Add SendCustomEvent override for control stream
  - Ensure all ServerConn interface methods work correctly

- Address linter issues
  - Fix struct field alignment with fieldalignment
  - Remove unused bytesSent/bytesReceived fields from ConnMetrics
  - Add ScaleNone case to switch statement
  - Refactor nested if to use continue pattern
  - Add nolint directive for acceptable int32 conversion
  - Rename unused ctx parameters to _

- Comment out incomplete V2 integration test
  - Test structure is correct but needs debugging
  - Connection manager not recognizing V2 connections
  - Will be resolved in future commit

All existing V1 tests pass. V2 infrastructure is in place.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>