<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--actions--delegator--random/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--actions--delegator--random/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step points to a tag, not a full 40-character commit SHA: `uses: slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0`. Tags can be moved, so the code that runs could change without this file changing.

Locations:

- `action.yml:34`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned slsa-framework/slsa-github-generator/.github/actions/rng from v2.1.0 to f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, with a '# v2.1.0' comment.

