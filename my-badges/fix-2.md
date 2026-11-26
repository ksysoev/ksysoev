<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/duet.nvim/commit/57daa02371716049e8cfe50f6fb6b6dbec9e1723">57daa02</a>: Fix second review findings for the split cap

A restart that reused a window of the user's, one that showed the
agent terminal, tagged it with the configured layout and winfixwidth.
With the cap, duet then sized that window as the panel, e.g. forced it
to 80 columns. A reused window now keeps only a layout duet gave it;
any other one gets just the display options.

A hand size is now used only under the size option it was recorded
with, so a setup() that changes split.width or split.height takes
effect on the next resize instead of keeping the old hand size.

split_cap() defaults keep to 0, so win_config() still works with a
split table that has no min_code_* keys.

The docs no longer claim that every change outside an editor resize
is noticed: one made in the same tick as an editor resize is not.
- <a href="https://github.com/ksysoev/duet.nvim/commit/f777b19f887e5f611047ee88eb5c039b9166705b">f777b19</a>: Fix review findings for the split cap

Telling a hand resize from duet's own sizes on VimResized compared the
split's size with the last one duet set. By then Neovim has already
redistributed the windows, and when min_code_width is below
winminwidth it shrinks the winfixwidth panel itself, which looked like
a hand resize: the panel never grew back. A hand size that got capped
was also recorded as duet's, so the panel later grew to the configured
size instead of the user's.

Detect hand resizes when they happen, on WinResized, and keep them in
w:duet_hand. On VimResized the split gets split_target(): the hand
size or the configured one, capped, and whatever size results is
recorded as duet's.

On an editor too small for both, the cap left the panel 1 cell wide.
split_cap() now shares the editor evenly below 2 * keep + 1 cells.

Also reject an infinite min_code_width or min_code_height, and
document that other sidebars are not counted.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>