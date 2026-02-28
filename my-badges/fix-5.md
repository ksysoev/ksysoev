<img src="https://my-badges.github.io/my-badges/fix-5.png" alt="I did 5 sequential fixes." title="I did 5 sequential fixes." width="128">
<strong>I did 5 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/6a740e7f137f3d9ae97577b4671fe88ed295fdb2">6a740e7</a>: Fix scroll-spy stale active heading by tracking intersection state across callbacks
- <a href="https://github.com/ksysoev/omnidex/commit/9198b6f0c3188f4aafa4a76b33cd0101fef03869">9198b6f</a>: Fix stale TOC observer cleanup and eliminate double markdown parse

Move observer disconnect to top of initScrollSpy() so navigating away
from a doc page always cleans up the previous IntersectionObserver
instead of leaving it attached to detached heading nodes.

Add ToHTMLWithHeadings() that parses markdown once, extracts headings
from the AST, then renders to HTML — replacing the separate ToHTML +
ExtractHeadings calls in GetDocument that parsed the source twice.
- <a href="https://github.com/ksysoev/omnidex/commit/0676d39c86605808598109eebc4dd07decf680ee">0676d39</a>: Fix TOC scroll-spy flicker and CSS selector injection in heading IDs
- <a href="https://github.com/ksysoev/omnidex/commit/3c86fdf05ad9075c4daf57b1b9854033231b7b84">3c86fdf</a>: Fix TOC accessibility: add IntersectionObserver guard, respect reduced-motion, and fix H1 indent spacing
- <a href="https://github.com/ksysoev/omnidex/commit/3393cca59fbbbb74fcb94884ddd390d0c7276fc9">3393cca</a>: Fix TOC review issues: accessibility, heading text extraction, indent hierarchy, and safe hash navigation


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>