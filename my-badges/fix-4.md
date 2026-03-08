<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/2e6af0b6450905bd646e8335ae8b1ddf14f6e55a">2e6af0b</a>: fix: align Scalar dark-mode surfaces with gray-800 card wrapper

Swap --scalar-background-1/2 so Scalar's primary surface (gray-800)
matches the card wrapper and other dark UI cards, while secondary/nested
surfaces recede to gray-900. Update sidebar variables and .scalar-card
wrapper background accordingly. Restore dark:bg-gray-800 on the wrapper
div for consistency with the rest of the portal.
- <a href="https://github.com/ksysoev/omnidex/commit/d913878e6ad8f65e8eaa2ae26897a68492a20833">d913878</a>: fix: use customCss to isolate Scalar theming from Tailwind wildcard

Tailwind's selector-based dark mode generates [data-theme=dark] * which
matches every descendant of <html data-theme="dark">, including all of
Scalar's internal elements. This caused dark:bg-* utility classes on the
card wrapper to force background-color onto every element Scalar renders,
fighting Scalar's own CSS variable theming.

Fix in three parts:
1. Move all Scalar CSS variable overrides (light-mode, dark-mode, sidebar,
   font/radius) into the customCss option of Scalar.createApiReference().
   Scalar injects customCss in its own rendering scope, bypassing the
   Tailwind wildcard entirely.
2. Replace dark:bg-gray-900 on the card wrapper with a plain CSS class
   (scalar-card) and a [data-theme=dark] .scalar-card rule in input.css.
   Plain class selectors are not affected by the Tailwind wildcard.
3. Remove all #scalar-api-reference blocks from input.css — they are
   no longer needed and were subject to Tailwind's optimizer stripping
   ancestor guards.
- <a href="https://github.com/ksysoev/omnidex/commit/70b6afac06da1652bf1581df58aecc301693301b">70b6afa</a>: fix: set Scalar root element background in dark mode

The #scalar-api-reference root element sits outside Scalar's own .dark-mode
subtree, so --scalar-background-1 CSS variables do not reach it. It was
rendering with the page-level --color-bg (#030712, gray-950) instead of the
intended gray-900 (#111827), creating a visible seam against the card wrapper.

Add a standalone [data-theme="dark"] #scalar-api-reference { background-color }
block. Because it is a separate block with a distinct property, Tailwind v3
does not merge it with the unguarded #scalar-api-reference blocks above, so
the guard survives compilation.
- <a href="https://github.com/ksysoev/omnidex/commit/4d5ceb7cf8a1a8061dbdd45d5087a428ef2b97da">4d5ceb7</a>: fix: resolve Scalar dark-mode background mismatch with card wrapper

Use html[data-theme="dark"] (element+attr selector) instead of [data-theme="dark"]
for Scalar CSS variable blocks so Tailwind v3's optimizer cannot collapse them
into the unguarded #scalar-api-reference rules above, which caused dark variables
to leak into light mode.

Change card wrapper from dark:bg-gray-800 (#1f2937) to dark:bg-gray-900 (#111827)
to match Scalar's --scalar-background-1 primary surface in dark mode, eliminating
the visible seam between the card and the Scalar component background.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>