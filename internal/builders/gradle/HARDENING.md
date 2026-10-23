<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--internal--builders--gradle/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--internal--builders--gradle/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### github-env-injection (severity: high)

The 'Run gradle builder' step writes `echo "validated_project_root=${project_root}" >> "${GITHUB_OUTPUT}"`. project_root comes from UNTRUSTED_PROJECT_ROOT (fromJson(inputs.slsa-workflow-inputs).directory) via realpath. It is written without the required `printf '%s' ... | tr -d '\n\r'` sanitization, so a directory name containing a newline could inject extra outputs.

Locations:

- `action.yml:95`

### unpinned-uses (severity: high)

Composite action steps use tag refs instead of full commit SHAs: `uses: slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0` and `uses: slsa-framework/slsa-github-generator/.github/actions/secure-upload-folder@v2.1.0`.

Locations:

- `action.yml:104`
- `action.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** github-env-injection, unpinned-uses

**Notes:**

Two fixes in action.yml. First, the 'Run gradle builder' step now removes newline and carriage-return characters from project_root (using printf '%s' | tr -d '\n\r') before writing validated_project_root to GITHUB_OUTPUT. The realpath capture stays a separate command, so if realpath fails the step still stops (errexit). Second, I looked up the commit SHA for tag v2.1.0 and pinned the rng and secure-upload-folder references to f7dd8c54c2067bafc12ca7a55595d5ee9b75204a, with a '# v2.1.0' comment.

