---
name: update-github-info
description: Refresh Mona's GitHub information page from GitHub and Awesome Copilot updates.
intent: Update the GitHub information page with concise, practical information from GitHub and Awesome Copilot sources and propose the changes for Mona's review.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - github.blog
    - awesome-copilot.github.com
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    reviewers:
      - monalisa
---

# Update GitHub Info

1. Read `notes/mona-notes.md` and follow Mona's editorial guidance.
2. Use web fetch to read `https://github.blog/latest/`.
3. Use web fetch to read `https://github.blog/changelog/`.
4. Use web fetch to read `https://awesome-copilot.github.com/workflows/`.
5. Update only `site/content/github-info.md` with short, practical information that helps developers learn GitHub faster. Preserve useful existing content and clearly cite the source for each new or changed item.
6. Use the configured `create-pull-request` safe output to propose the update for Mona's review. Do not create a pull request through any other tool or command.
7. If the source pages provide no useful update, the required files are unavailable, or the target content does not need a change, call `noop` with a brief reason.
