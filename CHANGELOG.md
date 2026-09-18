# 18/Sep/2026

- Fix: dynos not selected by `DEPENDENCIES_NEXT_DYNOS`/`DEPENDENCIES_NEXT_CI_NODES` could still boot
  with `Gemfile.next`. `BUNDLE_BIN=vendor/bundle/bin` on the `Gemfile.next` install regenerated the
  `bundle` binstub in `vendor/bundle/bin`, baking in `Gemfile.next` as its own fallback default
  (since that install runs with `BUNDLE_GEMFILE=Gemfile.next`). If nothing else on `PATH` shadowed
  that binstub, an unset `BUNDLE_GEMFILE` resolved to `Gemfile.next` instead of `Gemfile`. Dropped
  `BUNDLE_BIN` from that install (it doesn't need to generate binstubs) and `.profile.d` now
  explicitly exports `BUNDLE_GEMFILE=$HOME/Gemfile` for non-selected dynos/nodes instead of leaving
  it unset.

# 14/Sep/2026

- Bundler 4 support. `bundle install` uses inlined env vars instead of deprecated flags.

# 25/Apr/2025

- Delete git-related directories after bundle install to reduce slug size.
- Enable globstar so `**` behaves as expected when deleting `.git` directories.

# 26/Nov/2024

- Replace `Gemfile_next` with `Gemfile.next` (period replaces underscore). Also replace 
  `Gemfile_next.lock` with `Gemfile.next.lock`. This matches the more commonly seen naming
  standard.
