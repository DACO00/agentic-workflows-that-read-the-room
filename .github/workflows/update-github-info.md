---
name: update-github-info
description: Keep Mona's GitHub Info content current with official GitHub and Awesome Copilot updates.
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
    - awesome-copilot.github.com
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
4. Fetch and read `https://awesome-copilot.github.com/workflows/` with the web-fetch tool.
5. Review the current `site/content/github-info.md` using the GitHub repository API tools.
6. Update `site/content/github-info.md` with concise, practical, developer-focused summaries of relevant new GitHub Blog, Changelog, and Awesome Copilot workflow items. Preserve useful existing content, cite the source URL for every new item, and do not invent details.
7. Use the edit tool to make the file change. Do not modify other files.
8. If the file needs an update, use the `create-pull-request` safe output to open a draft pull request for Mona to review. Include a concise summary of the sources checked and the changes proposed in the pull request body. Never write directly to `main`.
9. If no meaningful update is available, do not create a pull request.
