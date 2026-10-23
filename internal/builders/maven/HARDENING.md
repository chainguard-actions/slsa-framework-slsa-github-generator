<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--internal--builders--maven/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--internal--builders--maven/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml has three uses: references that point to a version tag instead of a full 40-character commit SHA: 'uses: slsa-framework/slsa-github-generator/.github/actions/secure-builder-checkout@v2.1.0' (line 66), 'uses: slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0' (line 116), 'uses: slsa-framework/slsa-github-generator/.github/actions/secure-upload-folder@v2.1.0' (line 120). The actions/checkout and actions/setup-java references are pinned to SHAs.

Locations:

- `action.yml:66`
- `action.yml:116`
- `action.yml:120`

### script-injection (severity: high)

Sub-rule (b), unquoted expansion of untrusted data. In the 'Run mvn package' step, the result of a command substitution built from SLSA_OUTPUTS_ARTIFACTS_FILE is expanded without quotes. That variable comes from inputs.slsa-layout-file. Offending line: '[[ $(dirname "${SLSA_OUTPUTS_ARTIFACTS_FILE}") -ef "${GITHUB_WORKSPACE}/../" ]] || mv $(dirname "${SLSA_OUTPUTS_ARTIFACTS_FILE}") "${GITHUB_WORKSPACE}/../"'. Because the outer $(dirname ...) in the mv argument is unquoted, the shell splits it into words and expands glob characters, so an attacker-chosen path can add extra arguments or options to mv. Fix: write it as mv "$(dirname "${SLSA_OUTPUTS_ARTIFACTS_FILE}")" ...

Locations:

- `action.yml:109`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, script-injection

**Notes:**

Pinned the secure-builder-checkout, rng and secure-upload-folder sub-actions to commit f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, which lookup_action_sha returned for tag v2.1.0. Each line keeps a '# v2.1.0' comment. The checkout step's 'ref: v2.1.0' input is unchanged. In the 'Run mvn package' step, both $(dirname ...) substitutions are now double-quoted, so the mv argument can't be split into extra words or glob-expanded.

### Iteration 2

**Fixes applied:** unpinned-uses

**Notes:**

Pinned slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0 to f7dd8c54c2067bafc12ca7a55595d5ee9b75204a (# v2.1.0) in action.yml. This is the same SHA the secure-upload-folder step already uses.

