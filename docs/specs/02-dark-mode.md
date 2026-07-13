# Feature: Dark mode

## Behavior
- First visit: follow the OS preference (`prefers-color-scheme`).
- A ☾/☀ toggle in the nav overrides it; the choice persists in
  `localStorage.theme` and wins on subsequent visits.

## Implementation
The Sass color variables are compile-time, so rather than refactoring every
partial to CSS custom properties (and breaking the `lighten()`/`darken()`
calls), dark mode is a single override sheet keyed off a `data-theme`
attribute on `<html>`:

- `_sass/_dark.scss` — `html[data-theme="dark"] { … }` overrides for body,
  links, header/footer chrome, nav menu, search input, tag/school lists,
  blockquotes, and code blocks (~50 lines). Imported from `css/main.scss`.
- `_includes/head.html` — 4-line inline script, placed **before** the
  stylesheet link so there's no light-mode flash, that stamps `data-theme`
  from `localStorage` or the media query. Plus a click handler for the toggle
  registered in the existing `window.onload`.
- `_includes/header.html` — one `<a id="themeToggle">` nav link.

No new dependencies, no framework, degrades to light mode with JS disabled.

## Drive-by fixes bundled here
- Typekit loaded over `http://` — blocked as mixed content on the https site
  (fonts silently fall back). Switched to `https://`.
- `window.onload` assumed `.schools-list` exists; on spell pages it doesn't,
  so the handler threw and killed any JS after it. Now null-guarded.
