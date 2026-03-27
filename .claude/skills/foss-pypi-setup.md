# foss-pypi-setup — First-Time PyPI Publishing Setup

Set up automated PyPI publishing for a new package using trusted publishers (OIDC). No API tokens needed.

## Trigger

User says `/foss-pypi-setup` or asks to set up PyPI publishing, get a package on PyPI, or configure trusted publishing.

## Instructions

### Step 1: Check Current State

Determine which situation applies:

| Situation | How to detect | Path |
|-----------|--------------|------|
| Already on PyPI, no trusted publisher | `pip install <pkg>` works, but publish workflow fails with "invalid-publisher" | → Configure existing project |
| Never on PyPI | `pip install <pkg>` fails with "No matching distribution" | → Create pending publisher |
| Already on PyPI with trusted publisher | Publish workflow succeeds | → Done, nothing to do |

### Step 2a: Package Already on PyPI

1. Direct user to: `https://pypi.org/manage/project/<package-name>/settings/publishing/`
2. Add trusted publisher with these values:
   - **Owner:** the GitHub org (e.g., `eidos-agi`)
   - **Repository:** the repo name (e.g., `resume-resume`)
   - **Workflow name:** `publish.yml`
   - **Environment name:** `pypi`
3. Re-run the failed workflow: `gh run rerun <run-id>`

### Step 2b: Package NOT on PyPI (First Publish)

1. Direct user to: `https://pypi.org/manage/account/publishing/`
2. Under "Add a new pending publisher", fill in:
   - **PyPI project name:** the package name from `pyproject.toml` (e.g., `forge-forge`)
   - **Owner:** the GitHub org (e.g., `eidos-agi`)
   - **Repository:** the repo name (e.g., `forge-forge`)
   - **Workflow name:** `publish.yml`
   - **Environment name:** `pypi`
3. Click "Add"
4. Push a version tag: `git tag -a v<version> -m "Release v<version>" && git push --tags`
5. The publish workflow creates the PyPI project automatically on first run

### Step 3: Verify Publish Workflow Exists

Check for `.github/workflows/publish.yml`. If missing, create from foss-forge template:

```yaml
name: Publish to PyPI

on:
  push:
    tags: ["v*"]

jobs:
  publish:
    runs-on: ubuntu-latest
    environment: pypi
    permissions:
      id-token: write
      contents: read
    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install build tools
        run: pip install build

      - name: Build package
        run: python -m build

      - name: Publish to PyPI
        uses: pypa/gh-action-pypi-publish@release/v1
```

### Step 4: Verify

After the workflow succeeds:

```bash
pip install <package-name>==<version>
```

### Batch Mode

For multiple packages at once, collect the list and generate all the pending publisher entries. The user configures them on PyPI, then you tag and push each one.

## Rules

- **Never use API tokens.** Trusted publishing (OIDC) is the standard. No `.pypirc`, no `TWINE_PASSWORD`, no secrets.
- **Never skip the `environment: pypi` field.** The OIDC exchange requires it.
- **Pending publishers are the first-publish path.** No manual `twine upload` needed.
- **Private packages don't go on PyPI.** If the repo is private and should stay private, skip it.
