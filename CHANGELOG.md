# 21/Sep/2026

- Always set `BUNDLE_GEMFILE=Gemfile` unless in a `Gemfile.next` environment. Previously `BUNDLE_GEMFILE` would not
  be set.
- Generate `Gemfile.next`-hardcoded binstubs in the new directory `vendor/bundle/bin.next` instead of replacing
  `Gemfile`-hardcoded binstubs generated in `vendor/bundle/bin` by the Heroku Ruby buildpack. Please note
  `vendor/bundle/bin.next` is **not** on the `PATH`.
- These above two changes resolve a bug after deleting `bin/bundle` from your app as recommended by Heroku, which would
  cause `Gemfile.next` to be used for any `bundle exec` commands regardless of the `DEPENDENCIES_NEXT_DYNOS` value.
  Thank you to [Stefan Richter @stoem](https://github.com/stoem) for your work on fixing this.


# 14/Sep/2026

- Bundler 4 support. `bundle install` uses inlined env vars instead of deprecated flags.

# 25/Apr/2025

- Delete git-related directories after bundle install to reduce slug size.
- Enable globstar so `**` behaves as expected when deleting `.git` directories.

# 26/Nov/2024

- Replace `Gemfile_next` with `Gemfile.next` (period replaces underscore). Also replace 
  `Gemfile_next.lock` with `Gemfile.next.lock`. This matches the more commonly seen naming
  standard.
