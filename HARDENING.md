<!-- markdownlint-disable -->

# Hardening Report: seek-oss--changesets-snapshot/v0.3.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **seek-oss--changesets-snapshot/v0.3.2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable version tags instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag can be silently moved to point to malicious code.

.github/workflows/release.yml failing references:
- uses: actions/checkout@v6
- uses: pnpm/action-setup@v5
- uses: actions/setup-node@v6
- uses: changesets/action@v1

.github/workflows/validate.yml failing references:
- uses: actions/checkout@v6
- uses: pnpm/action-setup@v5
- uses: actions/setup-node@v6

All of these should be pinned to a full 40-character commit SHA (e.g. uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4).

Locations:

- `.github/workflows/release.yml:14`
- `.github/workflows/release.yml:19`
- `.github/workflows/release.yml:22`
- `.github/workflows/release.yml:29`
- `.github/workflows/validate.yml:13`
- `.github/workflows/validate.yml:22`
- `.github/workflows/validate.yml:25`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 7 unpinned action references across both workflow files to full 40-character commit SHAs:

.github/workflows/release.yml:
- actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
- pnpm/action-setup@v5 → @fc06bc1257f339d1d5d8b3a19a8cae5388b55320 # v5
- actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 # v6
- changesets/action@v1 → @a45c4d594aa4e2c509dc14a9f2b3b67ba3780d0d # v1

.github/workflows/validate.yml:
- actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
- pnpm/action-setup@v5 → @fc06bc1257f339d1d5d8b3a19a8cae5388b55320 # v5
- actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 # v6

All SHAs were resolved using lookup_action_sha. Original version tags are preserved as inline comments for readability.

