<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/mimir/commit/f7175a8ec5174dab902b23a6bcdd867025155b05">f7175a8</a>: fix: address PR review comments

- init_test.go: replace no-op assert.Contains(x, "") with assert.NotEmpty
  for cmd.Short and cmd.Long so regressions in descriptions are caught
- health_test.go: replace hardcoded 127.0.0.1:1 with httptest.NewServer+Close
  pattern to avoid flakiness on privileged/restricted environments
- docker.yml: remove environment: from build-and-push job; empty string is
  invalid in GitHub Actions and caused workflow validation failures on
  non-tag runs; environment scoping lives only on the deploy job
- deploy/docker-compose.yml: use :? syntax for API_KEY and MIT_TOKEN so
  Compose hard-fails with a clear error when required secrets are missing
  instead of silently running with an empty/disabled auth key
- deploy/docker-compose.yml: remove depends_on from mit-client as it is
  ignored by docker stack deploy (Swarm); add comment explaining that
  ordering is handled by the restart policy
- <a href="https://github.com/ksysoev/mimir/commit/b25431474170b7de9a2e9fb61ccd43ffac6dca18">b254314</a>: fix: rename APIKey to Key to avoid API_API_KEY env var double prefix

Config field mapstructure tag changed from 'api_key' to 'key', so the
env var is now API_KEY instead of API_API_KEY.

- pkg/api/api.go: APIKey -> Key, mapstructure:"api_key" -> "key"
- pkg/api/mux.go: a.config.APIKey -> a.config.Key
- pkg/api/mux_test.go: Config{APIKey: ...} -> Config{Key: ...}
- deploy/docker-compose.yml: API_API_KEY -> API_KEY
- docker-compose.yml: API_API_KEY -> API_KEY
- .github/workflows/docker.yml: secrets.API_API_KEY -> secrets.API_KEY


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>