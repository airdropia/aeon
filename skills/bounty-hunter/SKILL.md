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

## Model gateway fallback

The primary model is the Magpie gateway (`MAGPIE_BASE_URL` + `MAGPIE_API_KEY`,
model `group/personal-cc`) — reachable only while the operator's PC is on.
If the gateway is unreachable (timeout, connection refused, 5xx), fall back to
the Gemini API directly using `GEMINI_API_KEY` with model `gemini-3.1-flash-lite`
(free tier, no card). Before starting work, probe the gateway with a single
`GET /models` request (2s timeout); on failure, use the Gemini fallback for the
whole run so the run never dies just because the PC is off.
