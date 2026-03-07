<img src="https://my-badges.github.io/my-badges/fix-6.png" alt="I did 6 sequential fixes." title="I did 6 sequential fixes." width="128">
<strong>I did 6 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/a07626a2d5451defbd48f500ecfc916a5a655709">a07626a</a>: fix: remove stale nolint:gosec directives from api.go, health.go, publish.go

These were missed in the previous commit — the gosec false-positives for
these files are now suppressed via .golangci.yml exclusion rules instead.
- <a href="https://github.com/ksysoev/omnidex/commit/4bbcd8643f2d74a005171d8b937150bffa8b7c82">4bbcd86</a>: fix: exclude version-dependent gosec false-positives in .golangci.yml

Different gosec versions bundled in golangci-lint v2.10 vs v2.11 fire
different rule IDs for the same code (G117/G703/G704/G706 locally vs
G118/G122 on CI), making nolint directives unworkable across both.

Replace per-line nolints with exclusion rules in .golangci.yml scoped
to each rule ID with an explanation:
- G117: config/CLI-flag struct fields named 'Key' are not secret leaks
- G118: cancel is always called in the goroutine before the test returns
- G122: WalkDir path passed directly to ReadFile without re-resolution
- G703: path traversal guarded by explicit '../' prefix check above
- G704: SSRF intentional — URL is operator-supplied in CLI tools
- G706: log values are WalkDir filesystem paths, not user-injected input
- <a href="https://github.com/ksysoev/omnidex/commit/0136c7ec51c3f70c64a5f52a756e62c518f8370f">0136c7e</a>: fix: suppress pre-existing gosec false-positives with correct rule IDs

- G117 on Config.APIKeys and publishFlags.APIKey: field names match gosec's
  secret-pattern heuristic but these are config/CLI-flag structs, not leaks
- G704 on http.DefaultClient.Do in health.go and httpClient.Do in publisher:
  both are CLI tools making operator-supplied requests; SSRF is intentional
- G703 on os.ReadFile(absPath) in publisher: path traversal is already
  guarded by the explicit "../" prefix check immediately above the call
- G706 on slog.Warn calls in publisher: log values are WalkDir filesystem
  paths from user config, not attacker-controlled input in this CLI context
- <a href="https://github.com/ksysoev/omnidex/commit/03899d223bafc91e5ac4ad25f79c7073d8e25b51">03899d2</a>: fix: address remaining PR review comments

- Remove three spurious //nolint:gosec directives with fabricated rule IDs
  (G118 on context.WithCancel, G122 on os.ReadFile) that nolintlint flagged
  as unused since gosec never reported those lines
- Expand chromaClassPattern comment to explain why the [a-z]{1,3} catchall
  is intentionally broad and why it remains safe under the bluemonday policy
- Replace hard-coded class="cl" test assertion with a regexp so the test
  does not break if Chroma renames token classes in a future version
- <a href="https://github.com/ksysoev/omnidex/commit/0b64f495b0c55aa60b700efd383754410e097e25">0b64f49</a>: fix: address PR review issues with Chroma syntax highlighting

- Move chroma/v2 and goldmark-highlighting/v2 to direct requires (go mod tidy)
- Expand chromaClassPattern to cover 4+ char Chroma wrapper classes (line, lnt,
  ln, hl, lnlinks, lntable, lntd) that bluemonday was silently stripping
- Scope global .bg CSS rule to .chroma .bg to prevent styling collisions
- Fix .prose pre code.chroma selector (no-op) to .prose pre.chroma code,
  matching the actual HTML structure Chroma emits
- Add tests: ChromaHighlighting, ChromaClassesSurviveSanitization,
  PlainFencedBlockNotHighlighted
- <a href="https://github.com/ksysoev/omnidex/commit/bad81a8188ef3eb9d74b138b8c258f0cd5034efd">bad81a8</a>: fix: resolve golangci-lint v2.11.1 failures

- Replace context.Background() with context.WithoutCancel(ctx) in API shutdown goroutine (G118)
- Add //nolint:gosec G118 to test files where cancel is called in a sibling goroutine
- Add //nolint:gosec G122 to WalkDir ReadFile call in publisher (path is root-provided)
- Remove stale //nolint:gosec directives that no longer match any triggered rule under v2.11.1


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>