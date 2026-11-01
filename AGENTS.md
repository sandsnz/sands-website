# Project working notes

## Required change workflow

- Before changing any file in this repository, present a concise implementation plan to the user.
- Do not modify repository files until the user authorizes that plan by replying with the exact gateway word `Execute`.
- Treat discussion, approval in other words, or requests to revise the plan as insufficient authorization to edit files.
- After an authorized change is complete, verify the work in proportion to its risk, commit all and only the completed change, and push the commit directly to `origin/main`.
- Report the verification performed, the commit hash, and the push result.

## GitHub authentication on this Windows host

- Do not assume that the installed GitHub connector provides Git commit or push operations. In this environment it may expose only read-oriented GitHub features.
- Use local Git for commits and GitHub CLI (`gh`) for GitHub authentication and repository operations.
- If `gh` is missing, install `GitHub.cli` from the `winget` source (specify `--source winget` if the Microsoft Store source fails).
- Authenticate with `gh auth login --hostname github.com --git-protocol https --web` and enable Git credential integration when prompted.
- GitHub credentials are stored in Windows Credential Manager. Sandboxed commands may incorrectly report an invalid token or `SEC_E_NO_CREDENTIALS`; rerun authentication checks and authenticated Git operations in an approved external command context rather than re-authenticating unnecessarily.
- Verify access without changing the repository: run `gh auth status`, check `gh repo view Sandsnz/sands-website --json nameWithOwner,viewerPermission,defaultBranchRef`, and finish with `git push --dry-run`.
- A working setup should show the `sandsnz` account, sufficient repository permission, and `Everything up-to-date` (or an accurate dry-run push plan). Never create a dummy commit merely to test authentication.
