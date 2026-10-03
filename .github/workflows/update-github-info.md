---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
    allowed-repos: ${{ github.repository }}
    min-integrity: approved
    allowed:
      - get_repository
      - get_file_contents
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
---

# Update GitHub Info

Keep the GitHub Info page current with concise, practical guidance for developers.

1. Read `notes/mona-notes.md` and follow Mona's editorial guidance.
2. Use the `web-fetch` tool to read https://github.blog/latest/.
3. Use the `web-fetch` tool to read https://github.blog/changelog/.
4. Use the GitHub repository API tools for all repository reads. Do not use shell commands, the GitHub CLI, or sandboxed commands to read repository guidance or reference files.
5. Before reading a file with `get_file_contents`, list its parent directory with `get_file_contents` and request only the metadata fields needed for the listing.
6. Read `site/content/github-info.md` and update it with short, practical summaries of relevant official GitHub Blog or Changelog items. Mention the source for every Blog or Changelog update.
7. Use the `edit` tool to modify only `site/content/github-info.md`. Preserve the existing Markdown structure and do not change unrelated files.
8. After making a meaningful update, use the `create_pull_request` safe output to open a pull request containing the change for Mona to review. Include a concise summary and the source URLs in the pull request body.

Do not write directly to the default branch. If there are no relevant updates or no meaningful change is needed, do not create a pull request.