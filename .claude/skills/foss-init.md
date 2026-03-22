# foss-init — Scaffold FOSS Community Health Files

Generate missing community health files from Eidos AGI templates. Only creates files that don't already exist — never overwrites.

## Trigger

User says `/foss-init` or asks to scaffold open-source files for a repo.

### Arguments

- No args: scaffold ALL missing files
- `license` — only LICENSE
- `changelog` — only CHANGELOG.md
- `contributing` — only CONTRIBUTING.md
- `coc` — only CODE_OF_CONDUCT.md
- `security` — only SECURITY.md
- `ci` — only .github/workflows/ci.yml
- `publish` — only .github/workflows/publish.yml
- `gitignore` — only .gitignore
- `all` — everything, including CI workflows

## Instructions

1. Detect the project name from `pyproject.toml` (`project.name`), or from the directory name if no pyproject.toml exists.
2. Detect the GitHub org/repo from git remote (`git remote get-url origin`), or ask if not available.
3. For each missing file, generate it from the templates below. **Never overwrite existing files.**
4. After creating files, run a quick summary of what was created.

## Templates

All templates live in the foss-forge repo at:
`~/repos-eidos-agi/foss-forge/templates/`

Read each template file from that directory and apply variable substitution:

| Variable | Source |
|----------|--------|
| `{{PROJECT_NAME}}` | From pyproject.toml `project.name` or directory name |
| `{{PROJECT_SLUG}}` | Lowercase, hyphenated version of project name |
| `{{GITHUB_ORG}}` | From git remote (default: `eidos-agi`) |
| `{{GITHUB_REPO}}` | From git remote |
| `{{YEAR}}` | Current year |
| `{{DATE}}` | Current date in YYYY-MM-DD format |
| `{{AUTHOR_NAME}}` | `Eidos AGI` |
| `{{AUTHOR_EMAIL}}` | `daniel@eidosagi.com` |

### Template files to read from foss-forge/templates/:

- `LICENSE.tmpl` → `LICENSE`
- `CHANGELOG.md.tmpl` → `CHANGELOG.md`
- `CONTRIBUTING.md.tmpl` → `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md.tmpl` → `CODE_OF_CONDUCT.md`
- `SECURITY.md.tmpl` → `SECURITY.md`
- `gitignore.tmpl` → `.gitignore` (merge with existing if present)
- `ci.yml.tmpl` → `.github/workflows/ci.yml`
- `publish.yml.tmpl` → `.github/workflows/publish.yml`

## pyproject.toml Fixes

If `pyproject.toml` exists, also check and offer to fix:

1. **Missing license field** — add `license = "MIT"`
2. **Missing classifiers** — add standard classifiers based on Python version and license
3. **Missing keywords** — ask user for 3-5 keywords
4. **Missing project.urls** — add Homepage and Repository URLs from git remote
5. **setuptools → hatchling migration** — if using setuptools, offer to switch build-system to hatchling (show the diff, ask before applying)

## Rules

- **Never overwrite existing files.** If a file exists, skip it and note "already exists."
- **For .gitignore:** if it exists, read it and only append missing entries from the template.
- **Ask before modifying pyproject.toml** — show the proposed changes and get confirmation.
- **Create .github/workflows/ directory** if it doesn't exist before writing workflow files.
- After scaffolding, suggest running `/foss-check` to verify the result.
