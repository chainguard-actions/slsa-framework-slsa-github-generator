<!-- markdownlint-disable -->

# Hardening Report: slsa-framework--slsa-github-generator--actions--generator--generic--create-base64-subjects-from-file/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **slsa-framework--slsa-github-generator--actions--generator--generic--create-base64-subjects-from-file/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two composite action steps reference actions by a version tag instead of a full 40-character commit SHA: line 31 `uses: slsa-framework/slsa-github-generator/.github/actions/rng@v2.1.0` and line 52 `uses: slsa-framework/slsa-github-generator/.github/actions/secure-upload-artifact@v2.1.0`.

Locations:

- `action.yml:31`
- `action.yml:52`

### github-env-injection (severity: high)

The 'Generate random name' step builds `name=$(basename "${UNTRUSTED_PATH}")` from `inputs.path`, which it receives through an env var. It then writes that value, plus RNG from steps.rng.outputs.random, to $GITHUB_OUTPUT without running the `printf '%s' ... | tr -d '\n\r'` sanitization step first: `echo "artifact_name=${name}-${RNG}" >> "$GITHUB_OUTPUT"` and `echo "filename=${name}" >> "$GITHUB_OUTPUT"`. A path containing a newline could inject extra output keys.

Locations:

- `action.yml:46`
- `action.yml:47`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, github-env-injection

**Notes:**

Pinned the rng and secure-upload-artifact sub-actions to commit f7dd8c54c2067bafc12ca7a55595d5ee9b75204a. I resolved that SHA from the v2.1.0 tag and kept '# v2.1.0' as a comment. Before the basename-derived name and the RNG value are written to $GITHUB_OUTPUT, they now go through printf '%s' | tr -d '\n\r' to strip newlines. That stops a path with a newline from adding extra output keys. Nothing was run to test this. The two sub-actions now point at a commit SHA instead of the v2.1.0 tag. I didn't check whether they behave any differently when called that way.

### Iteration 2

**Fixes applied:** github-env-injection

**Notes:**

Fixed both findings in action.yml. In the 'Generate random name' step, the file name and the random value (RNG) now have newlines and carriage returns removed (printf '%s' | tr -d '\n\r') before artifact_name and filename are written to $GITHUB_OUTPUT. In the 'Create object' step, the base64 value gets the same cleanup before it is written. Base64 text never contains newlines except as line wrapping, so removing them leaves the value intact. That includes the macOS branch, which doesn't pass -w0. Nothing was run to test the changes.

