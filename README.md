# GitHub Actions Workflow for Automated Releases

This repository includes a set of GitHub Actions workflows designed to automate the process of creating releases, managing pull requests, and ensuring that PR titles follow the Conventional Commit format.

## Workflow Overview

### 1. **Validate PR Title** 🔍

- **Purpose**: Ensures that PR titles follow the Conventional Commit format before merging.
- **Trigger**: Runs on `opened`, `edited`, and `synchronize` events of pull requests.
- **Key Features**:
  - Comprehensive validation of PR title format
  - Detailed error messages with examples
  - Supports optional scopes and breaking changes
- **Validation Rules**:
  - Title must follow the pattern: `type(scope)!: description`
  - Allowed types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `ci`, `build`, `revert`

**Example Valid PR Titles**:

- `feat: add user authentication`
- `fix(login): resolve password reset bug`
- `docs(readme): update installation guide`
- `refactor!: major system redesign`

### 2. **Create Release Candidate** 🚀

- **Purpose**: Automatically creates a new release candidate PR based on merged pull requests.
- **Trigger**: Runs on `push` to `master` or `main` branch.
- **Key Features**:
  - Semantic version bump based on commit types
  - Comprehensive changelog generation with emojis
  - Support for Conventional Commits with scopes
  - Automated PR creation for release candidate
  - Maintains changelog history across releases

**Versioning Logic**:

- `feat`: Minor version bump
- `fix`, `perf`, `style`, etc.: Patch version bump
- Any commit with `!`: Major version bump (breaking change)
- Supports scoped commits like `feat(core): new feature`

**Changelog Categories**:

- ✨ Features
- 🐛 Bug Fixes
- 📝 Documentation
- 💄 Styling
- ♻️ Refactoring
- ⚡ Performance
- 🤖 Tests
- 🔧 Chores
- 👷 CI/CD
- 📦 Build
- 🔥 Reverts

### 3. **Finalize Release** ⛵

- **Purpose**: Creates a GitHub release when a release candidate pull request is merged.
- **Trigger**: Runs on `pull_request` closure when merging release candidates.
- **Key Features**:
  - Automated version tracking
  - Release notes generation from changelog
  - Branch cleanup after release
  - Verification of changelog presence

## Setup Instructions

### 1. **Prerequisites**

- Enable Workflow Permissions
  1. In your repository, go to Settings → Actions → General → Workflow permissions.
  2. Select Read and write permissions for the GITHUB_TOKEN.
  3. Check Allow GitHub Actions to create and approve pull requests.
- No manual file creation needed - versioning and changelog are handled automatically

### 2. **Conventional Commits**

Commit types:

- `feat`: ✨ New features

  - `feat: add user profile page`
  - `feat(ui): implement dark mode toggle`
  - `feat(auth)!: redesign authentication system (breaking change)`

- `fix`: 🐛 Bug fixes

  - `fix: correct typo in footer`
  - `fix(api): handle null responses gracefully`

- `docs`: 📝 Documentation changes

  - `docs: update README with setup instructions`
  - `docs(architecture): add sequence diagram`

- `style`: 💄 Code formatting

  - `style: reformat code with Prettier`
  - `style(css): fix indentation`

- `refactor`: ♻️ Code restructuring

  - `refactor: extract user service`
  - `refactor(api)!: remove deprecated endpoints (breaking change)`

- `perf`: ⚡ Performance improvements

  - `perf: optimize image loading`
  - `perf(db): add indexing for queries`

- `test`: 🤖 Test-related changes

  - `test: add unit tests for auth module`
  - `test(ci): integrate Cypress tests`

- `chore`: 🔧 Maintenance tasks

  - `chore: update dependencies`
  - `chore(release): bump version to v1.2.0`

- `ci`: 👷 CI/CD pipeline changes

  - `ci: add GitHub Actions workflow for linting`
  - `ci(build): cache dependencies`

- `build`: 📦 Build system changes

  - `build: migrate to Webpack 5`
  - `build(docker): update base image to node:18`

- `revert`: 🔥 Revert previous changes
  - `revert: revert "feat: add experimental feature"`
  - `revert(auth): rollback auth changes`

**Breaking Change Indicator**: Use `!` after type or scope to indicate a breaking change

- `feat!: overhaul API`
- `refactor(core)!: drop support for v1`

### 3. **Release Process**

1. Create PRs with Conventional Commit format titles
2. Merge approved PRs into `master` or `main`
3. Release candidate PR will be automatically generated with:
   - Updated version number
   - Generated changelog (with emojis and categories)
   - Release notes including date
4. Review the release candidate PR
5. Merge the release candidate PR
6. GitHub Release will be automatically created with the changelog content

## Benefits

- Fully automated versioning
- Automatic changelog generation with emoji categorization
- Standardized release process
- Historical changelog maintenance
- Enforced commit and PR conventions
- Clear release history
- No manual version management needed
- Automated breaking change detection

Feel free to customize the workflows to fit your project's specific needs!
