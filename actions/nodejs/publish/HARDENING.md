<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--actions--nodejs--publish/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--actions--nodejs--publish/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two composite action steps point to a mutable version tag instead of a full 40-character commit SHA: 'uses: slsa-framework/slsa-github-generator/.github/actions/secure-download-artifact@v2.1.0' and 'uses: slsa-framework/slsa-github-generator/actions/nodejs/secure-attestations-download@v2.1.0'.

Locations:

- `action.yml:59`
- `action.yml:66`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned both slsa-framework/slsa-github-generator sub-action references (secure-download-artifact, secure-attestations-download) to f7dd8c54c2067bafc12ca7a55595d5ee9b75204a # v2.1.0.

### Iteration 2

**Fixes applied:** unpinned-uses

**Notes:**

Pinned slsa-framework/slsa-github-generator/.github/actions/secure-download-artifact in action.yml (line 59) to commit f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, with a '# v2.1.0' comment. I confirmed with lookup_action_sha that this is the v2.1.0 commit. It's the same SHA the action already uses for its other step from this repo.

