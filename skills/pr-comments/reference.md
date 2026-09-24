# Fetching PR/MR comments per platform

## GitHub (`gh`)

- **Install**: `brew install gh` (or see https://cli.github.com for other package managers).
- **Auth check** (only after a failed fetch): `gh auth login`.
- **Fetch**, current branch's PR: `gh pr view --comments`
- **Fetch**, specific PR: `gh pr view <number> --comments` (add `--repo org/repo` for a repo
  that isn't the current working directory).

## GitLab (`glab`)

- **Install**: `brew install glab` (or see https://gitlab.com/gitlab-org/cli for other package
  managers). For a self-managed instance, also set `GITLAB_HOST=<your-host>` or pass
  `--hostname <your-host>`.
- **Auth check** (only after a failed fetch): `glab auth login`.
- **Fetch**, current branch's MR: `glab mr view --comments`
- **Fetch**, specific MR: `glab mr view <number> --comments` (add `--repo org/repo` for a repo
  that isn't the current working directory).

## Azure DevOps (`az`)

There's no dedicated `az repos pr comment`/`view --comments` command, so this uses the generic
REST invoker instead.

- **Install**: `brew install azure-cli`, then `az extension add --name azure-devops`.
- **Auth check** (only after a failed fetch): `az login` (or `az devops configure --defaults
  organization=<org-url> project=<project>` if defaults aren't set).
- **Fetch** PR comment threads:
  ```
  az devops invoke \
    --area git --resource pullRequestThreads \
    --route-parameters project=<project> repositoryId=<repo-id> pullRequestId=<pr-id> \
    --organization <org-url> \
    --api-version 7.1
  ```
  This returns raw JSON: each thread has a `comments` array with `content` and `author`.
  Parse it directly rather than looking for a prettier flag, none exists.