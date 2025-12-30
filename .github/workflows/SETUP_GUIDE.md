# GitHub Actions Setup Guide

## PyPI Release Workflow Setup

To enable automatic PyPI releases, you need to set up a PyPI API token as a GitHub secret.

### Steps:

1. **Create a PyPI API Token**
   - Go to [PyPI Account Settings](https://pypi.org/manage/account/)
   - Navigate to "API tokens" section
   - Click "Add API token"
   - Give it a name (e.g., "castAway-release")
   - Set the scope to the entire project
   - Copy the generated token

2. **Add Token to GitHub Secrets**
   - Go to your GitHub repository
   - Navigate to Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `PYPI_API_TOKEN`
   - Value: Paste your PyPI API token
   - Click "Add secret"

3. **Create a Release**
   - Update the version in [`pyproject.toml`](pyproject.toml)
   - Commit your changes
   - Create and push a version tag:
     ```bash
     git tag v0.1.0
     git push origin v0.1.0
     ```

The workflow will automatically:
- Build the package
- Upload to PyPI
- Create a GitHub release with release notes
- Attach the built distribution files

## CI Workflow

The CI workflow runs automatically on:
- Every push to `main` and `develop` branches
- Every pull request to `main` and `develop` branches

It includes:
- **Testing**: Runs tests across Python 3.8-3.12
- **Linting**: Checks code style with black, isort, and flake8
- **Type Checking**: Validates type hints with mypy
- **Coverage**: Reports code coverage

## Development Dependencies

Install development dependencies:
```bash
pip install pytest pytest-cov flake8 black isort mypy
```

## Useful Commands

```bash
# Run tests with coverage
pytest --cov=castAway --cov-report=html

# Format code
black castAway/
isort castAway/

# Check code style
flake8 castAway/ --max-line-length=88

# Type check
mypy castAway/