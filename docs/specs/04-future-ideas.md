# Backlog: lightweight feature ideas (not implemented)

Ordered by value-per-line-of-code. None add dependencies.

1. **Show the spell source.** Every post already carries `source: PHB.241`
   front matter that is never rendered. One line in `_layouts/post.html`
   (`{{ page.source }}` under the title) surfaces it.
2. **A–Z index page.** The bestiary already has `byname.html` (all entries
   alphabetically with the jets.js search box). Copying it over gives the
   grimoire a "find a spell when you don't know its level" page for ~30 lines.
3. **Ritual / concentration badges.** Add `ritual` / `concentration` to post
   tags where applicable, and two entries in a data file so they render as
   filterable tags like schools do. Data-entry-heavy, code-light.
4. **Print stylesheet.** The bestiary's `main.scss` already hides
   header/footer under `@media print`; port it and add a page-break rule so a
   spell page prints as a clean handout card.
5. **Favicon** — one file plus one line in `head.html`.
6. **Level filter on class pages.** The class tag pages already have per-level
   anchors; a "hide other levels" checkbox à la the school filter would reuse
   the same `filterSpells` mechanism.

## Deliberately avoided (bloat)
Search-across-pages (needs an index build step or JSON dump), spell-slot
tracking (state/app territory), and swapping the `github-pages` gem for
modern Jekyll (dependency churn with no user-visible gain).
