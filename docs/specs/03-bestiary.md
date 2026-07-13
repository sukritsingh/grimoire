# Bestiary: fixes ported from the grimoire

The bestiary repo is a near-clone (green accent, creature types instead of
classes) but deploys differently: `rake genpublish` builds **locally** with
plain Jekyll (so `_plugins/tag_gen.rb` runs and `tags/*.html` exist on
`gh-pages`) and pushes `_site` to the `gh-pages` branch.

## Bug: `baseurl` commented out in `_config.yml`
`#baseurl: "/bestiary"` on master. The currently deployed site was built when
it was still set; the **next** `rake genpublish` would emit every stylesheet
and link rooted at `/` instead of `/bestiary/`, breaking the whole site.
Fix: restore `baseurl` (and `source-url`, commented out alongside it).

## Feature: dark mode
Same implementation as grimoire spec 02 (`_sass/_dark.scss`, head script,
nav toggle). The override sheet is accent-neutral, so it drops in unchanged.

## Kept as-is
- `tag_gen.rb` stays: the local-build deploy runs plugins, and the bestiary
  tag space (14 types × 6 sizes × ~30 CRs) is too big for static pages.
- Header already links `/tags/<tag>.html` — correct for this repo.

Branch: `claude/bestiary-fixes` in the bestiary repo.
