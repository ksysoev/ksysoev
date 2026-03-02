<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/f687c853ec89bab1573de68c9f57e7c81b729863">f687c85</a>: fix: address remaining PR review comments on heading anchor

- Update hash on successful copy so the <a> behaves as a real anchor
  link (URL bar updates, browser history entry, right-click 'Copy link
  address' reflects the correct section URL)
- Encode heading IDs with encodeURIComponent when constructing the
  clipboard URL and hash to handle any non-URL-safe characters
- Remove dead 'position: relative' rule on .prose h1/h2/h3 (never used
  since the icon uses inline-flex, not absolute positioning)
- <a href="https://github.com/ksysoev/omnidex/commit/8675540512748ffe1708aede22c26e33e6effce8">8675540</a>: fix: address PR review comments on heading anchor pointer-events and touch support

- Add pointer-events: none to hidden .heading-anchor to prevent invisible clicks near heading text
- Restore pointer-events: auto on all reveal states (hover, focus, copied)
- Add @media (hover: none) rule so icon stays visible on touch devices
- Add test assertion that initHeadingAnchors is present in full-page output
- <a href="https://github.com/ksysoev/omnidex/commit/55f226dd861d68b1cfbc0f6913dd829c03cf952a">55f226d</a>: fix: address PR review comments on heading anchor copy-link

- Use href.split('#')[0] for URL construction to preserve query params
- Extract fallbackCopy() and invoke it from writeText .catch handler
  so execCommand is a true fallback for both unavailable clipboard API
  and permission-denied rejections
- Scope .heading-anchor CSS rules under .prose to win specificity over
  .prose a and correctly apply text-decoration/color overrides
- Add :focus and :focus-visible states so the icon is visible and
  operable for keyboard users


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>