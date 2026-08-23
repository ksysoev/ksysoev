<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/mimir/commit/b2dac72d69c6b15354e3aeb145ceef3d6ccf3811">b2dac72</a>: fix: proxy timeout and NDJSON scanner limit in router

Two production-facing issues in the router:

1. routeKey had no effective upstream timeout.
   The &httputil.ReverseProxy{} was created without a Transport, so it
   used http.DefaultTransport (no ResponseHeaderTimeout, no overall
   request timeout). r.client (10s Timeout) was used only by
   fetchNodeKeys, not the proxy. A frozen node could hold the proxy
   goroutine until the server WriteTimeout (15s) expired.

   Fix: add proxyTimeout field to Router (default 10s). routeKey now
   derives a child context with that deadline via context.WithTimeout
   and passes req.WithContext(ctx) to the proxy. ReverseProxy propagates
   the request context to Transport.RoundTrip, so the upstream call is
   bounded regardless of what the node does.

2. bufio.Scanner in fetchNodeKeys had a silent 64 KB line limit.
   bufio.MaxScanTokenSize is 64 KB. A key producing an NDJSON line
   longer than 64 KB caused scanner.Err() = bufio.ErrTooLong, which
   was returned as nodeKeyResult.err and treated as a node failure —
   silently dropping that node's entire key list with a misleading error.

   Fix: add maxScanLineBytes = 1 MB constant and call scanner.Buffer
   after creating the scanner. Lines up to 1 MB are now scanned
   correctly; lines exceeding the new limit still return a clear error
   rather than the old silent-drop behaviour.

Add tests:
- TestRouteKey_TimeoutOnSlowNode: slow node returns 502 within timeout
- TestRouteKey_TimeoutRespected: fast node unaffected by timeout
- TestFetchNodeKeys_LongLineWithinLimit: 512 KB key scanned without error
- TestFetchNodeKeys_LineExceedsLimit: >1 MB line surfaces as explicit error
- <a href="https://github.com/ksysoev/mimir/commit/da74430ab1d620b274f444545c7adee07fc0f3b1">da74430</a>: fix: ROUTER_NODES env var parsing and add loadRouterConfig tests

Viper splits env var values on commas before mapstructure sees them,
shredding a JSON array like '[{"id":"n1","url":"..."}]' into individual
strings that cannot be decoded into []NodeConfig. This meant the cluster
docker-compose, which relied on ROUTER_NODES as a JSON array, could never
start the router.

Fix: capture ROUTER_NODES before Viper's unmarshal pass, unset it so
Viper doesn't try to decode it, then parse it as JSON ourselves and
populate cfg.Router.Nodes. The env var is restored in a defer so other
code sharing the process is unaffected.

Add TestLoadRouterConfig (7 table-driven cases):
- valid config file
- missing config file returns error
- unparseable config file returns error
- scalar env vars (ROUTER_LISTEN, ROUTER_KEY) override file values
- ROUTER_NODES as JSON array correctly populates []NodeConfig
- ROUTER_NODES invalid JSON returns clear parse error
- no config file, nodes from ROUTER_NODES env only

Update docker-compose.cluster.yml: use >- (no trailing newline) for
ROUTER_NODES and correct the comment to reflect the actual JSON parsing
mechanism rather than the incorrect Viper claim.
- <a href="https://github.com/ksysoev/mimir/commit/b587968eb3a2e05a306418682303c81ab8f4557a">b587968</a>: fix: address PR review comments

- fix: set X-Mimir-Missing-Nodes header before WriteHeader
  Collect failed node IDs in a pre-pass after wg.Wait() and before any
  write so the header is actually delivered to clients. Two-pass approach:
  first pass builds missing list and sets headers, second pass writes body.
  Add assertion to TestListKeys_PartialNodeFailure to verify the header is
  present in the response.

- fix: do not log API keys in debug output
  Replace slog.Any("config", cfg) in loadConfig and loadRouterConfig with
  explicit non-secret fields (listen address, max_keys / node count).
  Prevents Key and InternalKey from appearing in CI logs or log collectors.

- fix: correct env var name in api.Config.NodeID comment
  NODE_ID -> API_NODE_ID, matching the viper env mapping and the value
  already used correctly in docker-compose.cluster.yml.

- fix: remove unused NodeID field from inmemory.Config
  NodeID was never read by the store; the node identity flows through
  api.Config.NodeID -> listKeys handler -> svc.ListKeys(ctx, nodeID).
  The dead field was misleading and could cause silent misconfiguration.
- <a href="https://github.com/ksysoev/mimir/commit/8d58076cc8b208ffe57784e68881edeb8744e17c">8d58076</a>: fix: resolve all linter issues in multi-node implementation

- gofmt: fix const block alignment in router/config.go
- govet/fieldalignment: reorder struct fields in router.Config, router.Router,
  nodeKeyResult, api.Config, inmemory.Config for optimal padding
- gocritic/hugeParam: pass *Config by pointer in router.New and router.Run
- staticcheck SA1019: replace deprecated ReverseProxy.Director with Rewrite;
  use bare &httputil.ReverseProxy{Rewrite:...} to avoid Director/Rewrite conflict
- gosec G118: use context.WithoutCancel for shutdown timeout so the deadline
  is not immediately cancelled along with the parent ctx
- unused: remove dead keyLine struct from router/handler.go
- whitespace: remove spurious leading newline in fetchNodeKeys
- wsl_v5: add required blank lines in handler_test.go, router_test.go, svc_test.go
- nolintlint: add explanation to nolint:gocritic directive in hash_test.go
- prealloc: pre-allocate nodes3 slice with cap 4 in hash_test.go
- remove unused math import from hash_test.go


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>