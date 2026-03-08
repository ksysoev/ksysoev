<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/omnidex/commit/7c083fdf4e9e8056d62c99136141f88ee2112433">7c083fd</a>: fix: address PR review — aria-pressed toggle, RAF Mermaid re-render, remove stale _initialDark closure
- <a href="https://github.com/ksysoev/omnidex/commit/79eb3094716a9fa1bfe6fa0e0f758a8b6c97832f">79eb309</a>: fix: address PR review — duplicate Scalar listener, stale theme closure, button type, CSS comment
- <a href="https://github.com/ksysoev/omnidex/commit/b5123bf0a2bb3c982838384f88fe4df2337a608d">b5123bf</a>: fix: address PR review — storage guards, Scalar dark mode, XSS fix, dark chrome

- Wrap localStorage.getItem in FOUC script with try/catch to prevent
  SecurityError crashing <head> in restrictive browser contexts
- Wrap localStorage.setItem in initThemeToggle with try/catch so the
  theme attribute change and omnidex:themechange event always fire
- Refactor initScalar to accept forceDarkModeState argument; add
  omnidex:themechange listener that re-creates the Scalar instance with
  the correct dark/light state on every theme toggle
- Replace pre.innerHTML with pre.textContent in Mermaid re-render to
  close XSS vector (Mermaid reads textContent, no functional change)
- Add dark: Tailwind variants to body, nav, footer, all bg-white content
  panels, headings, breadcrumbs, sidebar, TOC, and sub-templates so the
  page chrome actually switches on theme toggle
- Update stale 'light mode only' comment in static/css/input.css


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>