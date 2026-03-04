<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/4a569c5be3857cee36e7bcfe42f2f444577f560a">4a569c5</a>: fix: use consistent folder label styling across repo index and sidebar nav

Both folder headings now use text-sm font-medium text-gray-500 with no
CSS uppercase transform. Previously the sidebar applied uppercase/tracking-
wider (nav-heading style) while the repo index used text-gray-600, causing
folder names to render in ALL CAPS in one place and as-is in the other.
- <a href="https://github.com/ksysoev/omnidex/commit/9b14b9884fe1298ed585b901f96c4411c1b40736">9b14b98</a>: fix: preserve full document path in DocNode to fix 404 broken links

BuildDocTree was stripping the leading path segment from Doc.Path when
grouping nested documents for recursion, so a doc at guides/setup.md
ended up with Doc.Path = "setup.md" — causing 404s when templates built
links from that truncated path.

Introduce an internal docEntry type that carries both the original
*DocumentMeta pointer (full path untouched) and a separate remainingPath
field used only for recursive grouping. The public Doc.Path is now always
the original unmodified path. Update tests to assert full paths.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>