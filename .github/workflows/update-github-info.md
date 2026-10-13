---
name: update-github-info
description: Refresh GitHub Info with useful, source-backed updates from the GitHub Blog and Changelog.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  bash:
    - cat
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    reviewers:
      - mona
    allowed-files:
      - site/content/github-info.md
---

Read `notes/mona-notes.md` and the current `site/content/github-info.md`.
Use web-fetch to read:

- https://github.blog/latest/
- https://github.blog/changelog/

Update `site/content/github-info.md` with concise, practical information that
helps developers learn GitHub faster. Include links to the original Blog or
Changelog source for each update, and preserve the existing editorial angle and
themes. Only include information supported by those sources; do not invent
details or repeat items already covered. If neither page contains a useful new
update, leave the file unchanged and do not open an empty pull request.

When there is a meaningful change, open one pull request assigned to `mona` for
review. Describe the update and link its sources in the pull request. Submit
changes only through the configured create-pull-request safe output; do not
write directly to `main`.
