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


### lint-python

Run Python linters.

Full example:

```yaml
name: Dependabot auto-merge
on: pull_request

jobs:
  lint-python:
    uses: knyghty/actions/.github/workflows/lint-python.yml@main
    with:
      black: true
      flake8: true
      isort: true
      mypy: true
      package-manager: pip
      python-version: "3.10"
      requirements-files: requirements.txt requirements-dev.txt
      system-dependencies: libproj-dev gdal-bin
```

Inputs:

- black: If `true`, will run black. Defaults to `false`.
- flake8: If `true`, will run flake8. Defaults to `false`.
- isort: If `true`, will run isort. Defaults to `false`.
- mypy: If `true`, will run mypy. Defaults to `false`.
- package-manager: The package manager to use.
  Only pip and pipenv are currently supported.
  Defaults to `pip`.
  Only used when isort or mypy are enabled.
- python-version: The Python version to use. Defaults to `3.10`.
- requirements-files: A space-separated list of requirements files to use.
  Defaults to `requirements.txt`.
  Only used when `package-manager` is set to `pip` and isort or mypy is enabled.
- system-dependencies: A space-separated list of system dependencies to install.
  Defaults to an empty string.
  Only used when mypy is enabled.

Some linters (isort and mypy) require Python depdencies to be installed to work.
Addtionally, mypy can require system depdencies to be installed as the Python
modules are imported during linting.
