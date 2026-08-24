<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/mimir/commit/490c9fbea0e61150408a976fd792ae931bea72e2">490c9fb</a>: fix: address PR review comments

1. pkg/cmd/health.go: return error on malformed JSON from application/json
   /livez response instead of silently falling back to plain-text 'Ok',
   which would produce a false-positive healthy result
   - pkg/cmd/health_test.go: add TestRunHealthCheck_MalformedJSON_ReturnsError

2. pkg/api/api.go: guard against nil *Config in New() to prevent panic
   on cfg.Listen dereference when caller passes nil
   - pkg/api/api_test.go: add TestNew_NilConfig; add require import

3. pkg/router/handler.go: use slog.ErrorContext(req.Context(), ...) in
   healthCheck JSON-encode error log to be consistent with all other
   handler logs and preserve request-scoped fields (e.g. request ID)
- <a href="https://github.com/ksysoev/mimir/commit/b4ee6d46143b2095449bad243311df2b7699fd06">b4ee6d4</a>: fix: resolve all golangci-lint issues

gofmt:
  - pkg/api/api.go: remove blank line after imports
  - pkg/cmd/health.go: realign trailing comments
  - pkg/router/handler_test.go: align struct literal fields

govet/fieldalignment:
  - pkg/api/api.go: reorder API and Config fields to minimise
    leading GC pointer bytes (fieldalignment -fix)
  - pkg/router/config.go: same for router Config

gocritic/hugeParam:
  - api.New: accept *Config instead of Config by value (88 bytes)
  - printLivezResponse: accept *livez.Response instead of value
    (80 bytes); update all call-sites accordingly

wsl_v5:
  - pkg/cmd/health.go: add blank lines above if and final
    fmt.Fprintf in printLivezResponse


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>