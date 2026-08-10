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

1. **Detect the language track** (see below). It decides which templates apply.
2. Detect the project name from the manifest for that track, or from the directory name if there is no manifest.
3. Detect the GitHub org/repo from git remote (`git remote get-url origin`), or ask if not available.
4. For each missing file, generate it from the templates below. **Never overwrite existing files.**
5. After creating files, run a quick summary of what was created.

## Language tracks

Detect by manifest, in this order. A repo with more than one manifest uses the one at the repo root.

| Track | Detect by | Project name from | Test command |
|-------|-----------|-------------------|--------------|
| `python` | `pyproject.toml` | `project.name` | `pytest` |
| `swift` | `Package.swift` | `name:` in the `Package(...)` initializer | `swift test` |

Default to `python` when nothing matches — it's the ecosystem most of these tools live in — but
say so in the summary rather than silently assuming.

## Templates

All templates live in the foss-forge repo at:
`~/repos-eidos-agi/foss-forge/templates/`

**Resolution order:** for each file, look for `templates/<track>/<name>.tmpl` first and fall back to
`templates/<name>.tmpl`. Track-specific templates exist only where the language actually differs —
LICENSE, CODE_OF_CONDUCT, SECURITY, and CHANGELOG are the same for everyone.

Read each template file from that directory and apply variable substitution:

| Variable | Source |
|----------|--------|
| `{{PROJECT_NAME}}` | From the track's manifest (see Language tracks) or directory name |
| `{{PROJECT_SLUG}}` | Lowercase, hyphenated version of project name |
| `{{GITHUB_ORG}}` | From git remote (default: `eidos-agi`) |
| `{{GITHUB_REPO}}` | From git remote |
| `{{YEAR}}` | Current year |
| `{{DATE}}` | Current date in YYYY-MM-DD format |
| `{{AUTHOR_NAME}}` | `Eidos AGI` |
| `{{AUTHOR_EMAIL}}` | `daniel@eidosagi.com` |

### Template files to read from foss-forge/templates/:

| Output | Shared template | `swift` override |
|--------|-----------------|------------------|
| `LICENSE` | `LICENSE.tmpl` | — |
| `CHANGELOG.md` | `CHANGELOG.md.tmpl` | — |
| `CODE_OF_CONDUCT.md` | `CODE_OF_CONDUCT.md.tmpl` | — |
| `SECURITY.md` | `SECURITY.md.tmpl` | — |
| `CONTRIBUTING.md` | `CONTRIBUTING.md.tmpl` | `swift/CONTRIBUTING.md.tmpl` |
| `.gitignore` (merge if present) | `gitignore.tmpl` | `swift/gitignore.tmpl` |
| `.github/workflows/ci.yml` | `ci.yml.tmpl` | `swift/ci.yml.tmpl` |
| publish workflow | `publish.yml.tmpl` → `.github/workflows/publish.yml` | `swift/release.yml.tmpl` → `.github/workflows/release.yml` |

## Manifest fixes

### `python` — pyproject.toml

If `pyproject.toml` exists, also check and offer to fix:

1. **Missing license field** — add `license = "MIT"`
2. **Missing classifiers** — add standard classifiers based on Python version and license
3. **Missing keywords** — ask user for 3-5 keywords
4. **Missing project.urls** — add Homepage and Repository URLs from git remote
5. **setuptools → hatchling migration** — if using setuptools, offer to switch build-system to hatchling (show the diff, ask before applying)

### `swift` — Package.swift

Package.swift carries far less metadata than pyproject.toml — there is no description, keyword,
or URL field to fix. Check the things that do exist:

1. **Missing `platforms:`** — a package without it builds against the oldest supported OS and fails
   confusingly on modern API. Add an explicit `platforms: [.macOS(.v14)]` (or the real minimum).
2. **`swift-tools-version`** — present on line 1 and not older than the API the code uses.
3. **No test target** — offer to scaffold `Tests/<Target>Tests/`. A package with no test target
   cannot pass the CI template.
4. **Executable with GUI-only surface** — if the package builds an app but no CLI target, WARN:
   agents can't drive a GUI. Suggest splitting the logic into a library target that both an
   executable and the app depend on.
5. **`Package.resolved`** — committed for apps and executables, ignored for libraries.

## Rules

- **Never overwrite existing files.** If a file exists, skip it and note "already exists."
- **For .gitignore:** if it exists, read it and only append missing entries from the template.
- **Ask before modifying pyproject.toml** — show the proposed changes and get confirmation.
- **Create .github/workflows/ directory** if it doesn't exist before writing workflow files.
- After scaffolding, suggest running `/foss-check` to verify the result.
