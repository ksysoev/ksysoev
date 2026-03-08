<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/48bbee64ec1aeec086c6a15e1fe1c94c61be55eb">48bbee6</a>: fix: distinguish code block background from prose surface in dark mode

Code blocks (.prose pre / .prose pre.chroma) shared the same #1f2937
background as the dark:bg-gray-800 prose container, making them
visually indistinguishable. Override to #0d1117 (GitHub darkest surface)
in dark mode. Mermaid pre keeps transparent background as before.
- <a href="https://github.com/ksysoev/omnidex/commit/0a17ab53f534fb432e0351446e667266d379cf88">0a17ab5</a>: fix: restore dark mode text color for prose markdown content

Add missing base color rule for .prose in dark mode so body text,
list items, and paragraphs are visible against the dark background.
Also add explicit color overrides for h1–h6, fix inline code selector
from :not(pre)>code to the simpler .prose code, and add th text color.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>