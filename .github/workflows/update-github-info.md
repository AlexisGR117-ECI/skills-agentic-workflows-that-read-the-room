---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
  workflow_dispatch:
  schedule:
    - cron: '17 9 * * *'
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
tools:
  bash: ["curl"]
  edit:
network:
  allowed:
    - github
    - awesome-copilot.github.com
---

# Update GitHub Info

Keep the GitHub Info page current with concise, practical guidance for developers.

1. Read `notes/mona-notes.md` and follow Mona's editorial guidance.
2. Use `curl -fsSL` to read https://github.blog/latest/.
3. Use `curl -fsSL` to read https://github.blog/changelog/.
4. Use `curl -fsSL` to read https://awesome-copilot.github.com/workflows/.
5. Use the GitHub repository API tools for all repository reads. Do not use shell commands, the GitHub CLI, or sandboxed commands to read repository guidance or reference files.
6. Before reading a file with `get_file_contents`, list its parent directory with `get_file_contents` and request only the metadata fields needed for the listing.
7. Read `site/content/github-info.md` and update it with short, practical summaries of relevant items from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows. Mention the source for every update.
8. Use the `edit` tool to modify only `site/content/github-info.md`. Preserve the existing Markdown structure and do not change unrelated files.
9. After making a meaningful update, use the `create_pull_request` safe output to open a pull request containing the change for Mona to review. Include a concise summary and the source URLs in the pull request body.

Do not write directly to the default branch. If there are no relevant updates or no meaningful change is needed, do not create a pull request.