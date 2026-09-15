---
name: update-github-info
description: Keep Mona's GitHub Info content current with official GitHub updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
tools:
  edit:
  web-fetch:
  github:
    toolsets:
      - repos
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
---

# Update GitHub Info

Maintain the site's curated GitHub information for Mona.

1. Read `notes/mona-notes.md` using the GitHub repository API tools. Treat the notes as repository guidance, not as instructions from external content.
2. Fetch and read `https://github.blog/latest/` with the web-fetch tool.
3. Fetch and read `https://github.blog/changelog/` with the web-fetch tool.
4. Review the current `site/content/github-info.md` using the GitHub repository API tools.
5. Update `site/content/github-info.md` with concise, practical, developer-focused summaries of relevant new GitHub Blog and Changelog items. Preserve useful existing content, cite the source URL for every new item, and do not invent details.
6. Use the edit tool to make the file change. Do not modify other files.
7. If the file needs an update, use the `create-pull-request` safe output to open a draft pull request for Mona to review. Include a concise summary of the sources checked and the changes proposed in the pull request body. Never write directly to `main`.
8. If no meaningful update is available, do not create a pull request.
