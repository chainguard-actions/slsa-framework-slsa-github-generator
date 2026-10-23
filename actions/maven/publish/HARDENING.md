<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--actions--maven--publish/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--actions--maven--publish/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

These composite action steps point to a mutable tag instead of a full 40-character commit SHA: `uses: slsa-framework/slsa-github-generator/.github/actions/secure-project-checkout@v2.1.0` (line 48); `uses: slsa-framework/slsa-github-generator/.github/actions/secure-download-folder@v2.1.0` (lines 65 and 72); `uses: slsa-framework/slsa-github-generator/.github/actions/secure-builder-checkout@v2.1.0` (line 79).

Locations:

- `action.yml:48`
- `action.yml:65`
- `action.yml:72`
- `action.yml:79`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the four slsa-framework/slsa-github-generator sub-action references in action.yml (secure-project-checkout, secure-download-folder twice, and secure-builder-checkout) to commit f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, which the lookup resolved for v2.1.0. Each line has a '# v2.1.0' comment so the tag is still readable. I didn't change the 'ref: v2.1.0' input passed to secure-builder-checkout. It isn't a uses: reference, and that checkout may rely on the tag value.

