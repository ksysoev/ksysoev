<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/chess-com/commit/4cbf59b89d8ab56d74ae5469631f54a5f0a67e92">4cbf59b</a>: fix: address remaining PR review comments

- Refactor options to use transient config struct, removing the timeout
  field from Client; WithTimeout and WithHTTPClient now behave correctly
  regardless of option application order
- Drain response body with io.Copy(io.Discard) on all non-OK paths in
  get() to allow HTTP/1.1 connection reuse
- Rename LiveKingOfHill to LiveKingOfTheHill to match the full API name
- Broaden dupl linter exclusion to cover all endpoint files
- <a href="https://github.com/ksysoev/chess-com/commit/10d33b79b1526961596c8b8095b254623d165f55">10d33b7</a>: fix: address PR review comments

- Rename TournamentSt to TournamentStats for clarity
- Remove in-memory ETag cache; delegate caching to callers via custom http.RoundTripper
- Fix WithTimeout order-dependency by storing duration and applying after all options in New()
- Refactor GetMonthlyArchivePGN to reuse c.get() instead of duplicating HTTP logic
- Simplify TestGetTeamMatch server setup using fmt.Sprintf path per test case
- Update client_test.go to reflect cache removal and add WithTimeout ordering guarantee test


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>