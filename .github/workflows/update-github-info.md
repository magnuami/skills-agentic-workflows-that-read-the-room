---
name: update-github-info
description: Propose practical, sourced updates to the GitHub Info website for Mona to review.
intent: Keep Mona's GitHub Info website current with concise, useful updates backed by official GitHub sources.
strict: true
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
tools:
  edit: true
  web-fetch:
  github:
    mode: gh-proxy
    toolsets: default
network:
  allowed:
    - github.blog
    - github.com
engine:
  id: copilot
  copilot-sdk: true
safe-outputs:
  create-pull-request:
    title-prefix: "[Mona] "
    allowed-files:
      - site/content/github-info.md
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md`. Fetch
https://github.blog/latest/ and https://github.blog/changelog/ with the web-fetch
tool. Use official source material to identify practical, developer-relevant
updates that fit the site's current themes. Keep summaries short, include a
source link for every blog or changelog update, preserve existing useful content,
and do not add details that the sources do not support.

Check open pull requests for an existing proposal covering the same updates.
Edit only `site/content/github-info.md`, and only when there is a useful,
well-supported update not already proposed. Then open one focused pull request
for Mona to review; make no direct GitHub writes or changes to `main`. Use the
configured `create-pull-request` safe output. If evidence is insufficient, the
updates are already represented, or no material edit is warranted, call `noop`
with a brief reason.
