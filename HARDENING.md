<!-- markdownlint-disable -->

# Hardening Report: seek-oss--changesets-snapshot/v0.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **seek-oss--changesets-snapshot/v0.2.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if any of these actions are compromised or their tags are moved. Failing references in release.yml: actions/checkout@v5 (line 18), pnpm/action-setup@v4 (line 22), actions/setup-node@v4 (line 25), changesets/action@v1 (line 37). Failing references in validate.yml: actions/checkout@v5 (line 17), pnpm/action-setup@v4 (line 20), actions/setup-node@v4 (line 23). All should be replaced with full 40-character hex commit SHAs (e.g. uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v5).

Locations:

- `.github/workflows/release.yml:18`
- `.github/workflows/release.yml:22`
- `.github/workflows/release.yml:25`
- `.github/workflows/release.yml:37`
- `.github/workflows/validate.yml:17`
- `.github/workflows/validate.yml:20`
- `.github/workflows/validate.yml:23`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 7 unpinned action references across .github/workflows/release.yml and .github/workflows/validate.yml:
- actions/checkout@v5 → @fbc6f3992d24b796d5a048ff273f7fcc4a7b6c09 # v5 (both files)
- pnpm/action-setup@v4 → @b906affcce14559ad1aafd4ab0e942779e9f58b1 # v4 (both files)
- actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020 # v4 (both files)
- changesets/action@v1 → @a45c4d594aa4e2c509dc14a9f2b3b67ba3780d0d # v1 (release.yml only)
Original version tags preserved as inline comments for readability.

