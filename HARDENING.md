<!-- markdownlint-disable -->

# Hardening Report: seek-oss--changesets-snapshot/v0.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **seek-oss--changesets-snapshot/v0.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable tag refs instead of pinned 40-character SHA commit hashes, making the workflows vulnerable to supply-chain attacks if the referenced action tags are moved or compromised.

.github/workflows/release.yml:
  - `uses: actions/checkout@v4` (line 18)
  - `uses: actions/setup-node@v4` (line 23)
  - `uses: changesets/action@v1` (line 33)

.github/workflows/validate.yml:
  - `uses: actions/checkout@v4` (line 16)
  - `uses: actions/setup-node@v4` (line 19)

Each should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/release.yml:18`
- `.github/workflows/release.yml:23`
- `.github/workflows/release.yml:33`
- `.github/workflows/validate.yml:16`
- `.github/workflows/validate.yml:19`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 5 unpinned `uses:` references to full 40-character SHA commit hashes:
- `.github/workflows/release.yml`: `actions/checkout@v4` → `@11d5960a326750d5838078e36cf38b85af677262 # v4`, `actions/setup-node@v4` → `@49933ea5288caeca8642d1e84afbd3f7d6820020 # v4`, `changesets/action@v1` → `@a45c4d594aa4e2c509dc14a9f2b3b67ba3780d0d # v1`
- `.github/workflows/validate.yml`: `actions/checkout@v4` → `@11d5960a326750d5838078e36cf38b85af677262 # v4`, `actions/setup-node@v4` → `@49933ea5288caeca8642d1e84afbd3f7d6820020 # v4`
All SHAs were resolved via lookup_action_sha. Original tags are preserved as inline comments for readability.

