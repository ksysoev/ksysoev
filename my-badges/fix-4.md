<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/make-it-public/commit/44a567f883c3759e933ebd03426e63beeb7c629b">44a567f</a>: Fix gosec warning in fmt_json.go

Add #nosec G705 to CLI output formatting in FormatInteractive method.
- <a href="https://github.com/ksysoev/make-it-public/commit/744b5cb52518cd6c24a214cdbd669e7c707a0ca6">744b5cb</a>: Fix final gosec warning in ws.go logHandshakeInteractive

Add #nosec G705 to second fmt.Fprintf call that also formats CLI output.
- <a href="https://github.com/ksysoev/make-it-public/commit/977b45f8ed5fceeb3db74b29f5b078d222ee4cd9">977b45f</a>: Fix remaining gosec warnings in srv.go and ws.go

- Add #nosec G705 for CLI output formatting in logInteractive and printHeaders
- Add #nosec G706 for structured logging in logHandshakeStructured

These are CLI tools that format output to stdout, not web applications,
so XSS and log injection are not applicable security risks.
- <a href="https://github.com/ksysoev/make-it-public/commit/30a19bc2055dcbc4286d92144e1d75b3a7191758">30a19bc</a>: Fix gosec security warnings with appropriate nosec comments

- Add #nosec G101 for test token fixtures in client_test.go
- Add #nosec G117 for config field names (Secret, Password) in token.go and auth.go
- Add #nosec G704 for localhost test HTTP request in srv_test.go
- Add #nosec G705 for CLI output formatting (not web XSS) in fmt_*.go and srv.go
- Add #nosec G706 for structured logging (not log injection risk) in srv.go and ws.go

All warnings were false positives for a CLI tool that doesn't handle untrusted web input.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>