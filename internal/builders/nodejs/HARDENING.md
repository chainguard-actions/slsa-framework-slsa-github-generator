<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--internal--builders--nodejs/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--internal--builders--nodejs/v2.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml has composite steps whose uses: refs are mutable tags, not 40-character commit SHAs: 'uses: slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0' and 'uses: slsa-framework/slsa-github-generator/.github/actions/secure-upload-artifact@v2.1.0'. Pin each one to a full commit SHA.

Locations:

- `action.yml:91`
- `action.yml:93`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the rng and secure-upload-artifact actions in action.yml to slsa-framework/slsa-github-generator@f7dd8c54c2067bafc12ca7a55595d5ee9b75204a (the commit that v2.1.0 resolves to), with a '# v2.1.0' comment after each so the version stays readable.

### Iteration 2

**Fixes applied:** github-env-injection

**Notes:**

generate-layout.sh: attestation_name (built from PACKAGE_FILENAME) is now passed through printf '%s' | tr -d '\n\r' before it is written as attestation-name to $GITHUB_OUTPUT. action.yml already maps the step output through env:, so it was left as it was.

