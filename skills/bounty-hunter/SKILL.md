---
name: bounty-hunter
description: Find, claim, fix, and submit TaskBounty bounties end-to-end on cloud.
mode: write
---
1. Use TaskBounty MCP tool `list_open_bounties` to fetch available bounties.
2. Pick ONE bounty with clear repro steps and existing tests (prefer TS/JS, Python, Go).
3. Use `request_repo_access` to get the short-lived clone URL.
4. Clone the repo. Reproduce the bug.
5. Write a fix AND a regression test (fails before fix, passes after).
6. Commit, push, and open a PR using `gh pr create`.
7. Use `submit_pr` with the PR URL to register the submission.
