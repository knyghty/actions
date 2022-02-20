# actions
Reusable workflows for GitHub Actions

## Available actions

### dependabot-auto-merge

Automatically reviews and/or merges dependabot pull requests.

Full example:

```yaml
name: Dependabot auto-merge
on: pull_request_target

jobs:
  dependabot-auto-merge:
    uses: knyghty/actions/.github/workflows/dependabot-auto-merge.yml@main
    with:
      review: false
      merge: true
      update-types: '["version-update:semver-patch"]'
```

Inputs:

- `review`: If `true`, will approve the pull request. Defaults to `true`.
- `merge`: If `true`, will set the pull request to be merged automatically.
  Defaults to `true`.
  Note this requires "Allow auto-merge" to be enabled in the repository settings.
- `update-types`: A stringified JSON array of update types to automatically merge / approve.
  Defaults to `'["version-update:semver-minor", "version-update:semver-patch"]'`.
  Note this must be provided as a string due to GitHub Actions limitations.
  Available update types:
  - `version-update:semver-major`: Semver major update (1.0.0 -> 2.0.0)
  - `version-update:semver-minor`: Semver minor update (1.0.0 -> 1.1.0)
  - `version-update:semver-patch`: Semver patch update (1.0.0 -> 1.0.1)
