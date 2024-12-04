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

- GitHub Personal Access Token (PAT) with:
  - `contents: write and read` permission
  - `pull-requests: write and read` permission
  - `NOTE:` This means when it creates the release-candidate PR, it will be assigned to this account. preferably use a service account.
- Add the PAT to your repository secrets as `PAT`
- No manual file creation needed - versioning and changelog are handled automatically

### 2. **Conventional Commits**

Commit types:

- `feat`: ✨ New features
- `fix`: 🐛 Bug fixes
- `docs`: 📝 Documentation changes
- `style`: 💄 Code formatting
- `refactor`: ♻️ Code restructuring
- `perf`: ⚡ Performance improvements
- `test`: 🤖 Test-related changes
- `chore`: 🔧 Maintenance tasks
- `ci`: 👷 CI/CD pipeline changes
- `build`: 📦 Build system changes
- `revert`: 🔥 Revert previous changes

**Breaking Change Indicator**: Use `!` after type or scope to indicate a breaking change

- Example: `feat(auth)!: redesign authentication system`

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
