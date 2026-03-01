<img src="https://my-badges.github.io/my-badges/fix-6.png" alt="I did 6 sequential fixes." title="I did 6 sequential fixes." width="128">
<strong>I did 6 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/c9740206367b33073a0167891e8c61d514c0f48d">c974020</a>: fix: add OpenAPI spec validation in parseSpec to reject invalid specs early
- <a href="https://github.com/ksysoev/omnidex/commit/d9b53a8adb88ed8183cdac479600672977285963">d9b53a8</a>: fix: remove dead spec validation and handle YAML flow-mapping detection
- <a href="https://github.com/ksysoev/omnidex/commit/36f5f86047e81ccdf2bc2a86964a38e9e80d4dcc">36f5f86</a>: fix: address review comments for OpenAPI template security and docs

- Replace template.JS bypass with <script type="application/json"> + JSON.parse()
  to eliminate XSS risk from raw JSON embedding
- Add #swagger-ui existence guard in initSwagger() to prevent runtime errors
  when HTMX navigation removes the element before async script loads
- Update ContentProcessor.RenderHTML doc comment to reflect polymorphic return
- Remove unused js template function
- <a href="https://github.com/ksysoev/omnidex/commit/28be5255949eb08a8fb10ea27ea34482932b2986">28be525</a>: fix: skip non-OpenAPI YAML/JSON, add Swagger 2.0 detection, normalize unknown content types

- DetectContentType returns empty for non-OpenAPI YAML/JSON so the
  publisher skips arbitrary config files instead of ingesting them as
  broken markdown (contradicted the issue #33 design).
- Add Swagger 2.0 ("swagger" key) detection alongside OAS 3.x.
- Normalize unknown content types to markdown in upsertDocument before
  persisting to keep stored data consistent with rendering behavior.
- Fix misleading Processor doc comment in openapi package.
- <a href="https://github.com/ksysoev/omnidex/commit/feab8239e8a1b9cd19565caa02962c930fd3d492">feab823</a>: fix: address PR review comments for OpenAPI support

- Fix HTMX partial rendering race condition by dynamically loading
  Swagger UI CSS/JS with dedup guards and onload-based initialization
- Remove unused SwaggerUIStandalonePreset from presets (BaseLayout only)
- Validate processors map in core.New() to fail fast on misconfiguration
- Fix kin-openapi go.mod annotation from indirect to direct dependency
- <a href="https://github.com/ksysoev/omnidex/commit/64bf9096792aec1ad538e3019818e414358bba65">64bf909</a>: fix: correct SRI integrity hashes for Swagger UI CDN resources


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>