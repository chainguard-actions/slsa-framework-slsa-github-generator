# Hardening Report: slsa-framework--slsa-github-generator--actions--delegator--secure-download-folder/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `c40cfe5fa14e08549b1b988e7e5a26da4816abf0`

**Test Policy SHA:** `f2e7d85641cde4267138117189b8eba7ba2bfbde`

Action **slsa-framework--slsa-github-generator--actions--delegator--secure-download-folder/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step uses a mutable version tag ref (@v2.1.0) instead of a pinned 40-character commit SHA. This means the referenced action could be silently replaced with malicious code without any change to this file, creating a supply-chain attack vector.

Failing reference:
  uses: slsa-framework/slsa-github-generator/.github/actions/secure-download-folder@v2.1.0

Remediation: Pin to a full commit SHA, e.g.:
  uses: slsa-framework/slsa-github-generator/.github/actions/secure-download-folder@<40-char-sha> # v2.1.0

Locations:

- `action.yml:34`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the mutable tag reference `slsa-framework/slsa-github-generator/.github/actions/secure-download-folder@v2.1.0` to the full commit SHA `f7dd8c54c2067bafc12ca7a55595d5ee9b75204a` with the original tag preserved as a comment (`# v2.1.0`).

