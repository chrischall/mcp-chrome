# CLAUDE.md

## This is a fork

This is a fork of [hangwin/mcp-chrome](https://github.com/hangwin/mcp-chrome).
Upstream owns the design, the docs, and the release process. Read
`README.md` and `docs/` as upstream material, not as ours.

- `origin` → `chrischall/mcp-chrome` (this fork)
- `upstream` → `hangwin/mcp-chrome`
- Default branch is `master` (not `main`).

## Our delta

Essentially none. `master` is upstream's `master` plus two merged
Dependabot bumps (uuid, vitest) — no intentional divergence.

The one real change lives on the branch
`feat/network-request-tab-targeting`, which is open upstream as
[PR #348](https://github.com/hangwin/mcp-chrome/pull/348): it adds
`tabId` / `tabUrl` / `windowId` targeting to the `chrome_network_request`
tool, so a request can be issued from a chosen tab instead of only the
active one.

## Why we maintain it

`~/git/opentable-mcp` supports `OT_BRIDGE=mcp-chrome`, which routes its
fetches through this project's HTTP MCP endpoint
(`http://127.0.0.1:12306/mcp`) as an opt-in alternative to its default
fetchproxy WebSocket bridge. That path depends on the `tabUrl` parameter
from PR #348 — without it mcp-chrome is active-tab-only and credentialed
cross-origin fetches break. So this fork exists to carry that patch until
(or unless) upstream merges it. See `~/git/opentable-mcp/CLAUDE.md`.

## Working here

Note that upstream's `.gitignore` deliberately ignores `CLAUDE.md`,
`Agents.md`, and `.claude/` — agent instruction files are not wanted in
their tree. This file is therefore force-added in our fork only. Leave
`.gitignore` alone, and do not carry this file into any PR we send to
hangwin/mcp-chrome.

Keep divergence from upstream to a minimum — every local change we do not
upstream makes the next merge from `upstream/master` harder. Prefer
sending changes to hangwin/mcp-chrome as PRs over accumulating them here.
Do not restyle, restructure, or apply our house conventions to upstream's
code or docs. Follow upstream's own conventions (pnpm workspace,
Conventional Commits enforced by commitlint, prettier/eslint configs in
the repo root).
