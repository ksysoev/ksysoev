<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/26b3853cac14a9610ae13f463abea766eae34b25">26b3853</a>: Fix security and code quality issues from PR review

Add bluemonday HTML sanitizer after goldmark rendering to prevent XSS
via crafted markdown content. Add path traversal protection in docstore
by validating resolved paths stay within the base directory. Replace
fragile string-based error matching with sentinel errors and errors.Is.
Use graceful HTTP server shutdown with timeout instead of immediate close.
Improve docstore test coverage from 66% to 82% and add mux route test.
- <a href="https://github.com/ksysoev/omnidex/commit/5ae91d927f150821f02b6581f6d8e6dd66976a6a">5ae91d9</a>: Fix CI: add missing objx indirect dependency required by mockery mocks


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>