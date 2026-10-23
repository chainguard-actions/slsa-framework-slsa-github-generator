<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--actions--delegator--secure-upload-folder/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--actions--delegator--secure-upload-folder/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

A composite step references an action by a version tag instead of a full 40-character commit SHA: `uses: slsa-framework/slsa-github-generator/.github/actions/secure-upload-folder@v2.1.0`

Locations:

- `action.yml:37`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned slsa-framework/slsa-github-generator/.github/actions/secure-upload-folder to f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, with a # v2.1.0 comment.

