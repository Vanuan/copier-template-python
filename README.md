# Python Package Template

[![Copier](https://img.shields.io/badge/made%20with-copier-blue)](https://copier.readthedocs.io/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

This is a **Copier template** for creating Python packages with best practices, including CI/CD, documentation, version management, and automated releases.

## Features

- **Pre-configured CI/CD workflows**:
  - Automated testing and linting.
  - Automated version bumping and releases.
  - Automated documentation deployment to GitHub Pages.
- **Documentation setup**:
  - Sphinx with ReadTheDocs theme.
  - Markdown and reStructuredText support.
- **Version management**:
  - Automated version bumping using `bump2version`.
  - GitHub Actions workflows for releasing to PyPI.
- **Customizable**:
  - Easily adapt the template to your project's needs.

## Getting Started

### Prerequisites

- Python 3.10 or newer.
- Git 2.27 or newer.
- [Copier](https://copier.readthedocs.io/) installed.

### Installation

1. Install Copier:
   ```bash
   pipx install copier
   ```

2. Generate a new project from this template:
   ```bash
   copier copy gh:vanuan/copier-template-python my-new-project
   ```

3. Follow the prompts to customize your project:
   - **Project Name**: The name of your project (e.g., `my-awesome-project`).
   - **Module Name**: The Python module name (e.g., `my_awesome_project`).
   - **Author Name**: Your GitHub name or organization.
   - **Author Email**: Your email address that will be published on PyPI.
   - **Python Version**: The Python version your project will use (e.g., `3.10`).
   - **License**: The license for your project (e.g., `MIT`).


## Initial Configuration

Before using the workflows, you need to configure the following **GitHub Secrets** and configure services:

### PyPI API Token
   - This token is used to upload your package to PyPI.
   - Steps to create and configure the token:
     1. Go to [PyPI](https://pypi.org/) and log in to your account.
     2. Navigate to **Account Settings** > **API Tokens**.
     3. Click **Add API Token** and create a new token with the scope `Entire account` (or restrict it to the specific project).
     4. Copy the token.
     5. Go to your GitHub repository's **Settings** > **Secrets and variables** > **Actions**.
     6. Click **New repository secret**.
     7. Set the **Name** to `PYPI_API_TOKEN` and paste the token as the **Value**.
     8. Click **Add secret**.

### GitHub Token
   - This token is used to create GitHub releases and upload assets.
   - Steps to configure the token:
     1. Go to your GitHub repository's **Settings** > **Secrets and variables** > **Actions**.
     2. Click **New repository secret**.
     3. Set the **Name** to `GITHUB_TOKEN`.
     4. The **Value** will be automatically populated by GitHub (no need to manually create a token).
     5. Click **Add secret**.

### Enable GitHub Pages
   - GitHub Pages is used to host your project's documentation.
   - Steps to enable GitHub Pages:
     1. Go to your GitHub repository's **Settings** > **Pages**.
     2. Under **Source**, select the `gh-pages` branch and `/ (root)` folder.
     3. Click **Save**.
     4. Wait a few minutes for GitHub to build and deploy your documentation.
     5. Access your documentation at `https://<your-username>.github.io/<your-repo-name>/`.

### Check Package Name Availability on PyPI
   - Before releasing your package, ensure the name is available on PyPI.
   - Steps to check availability:
     1. Go to [PyPI](https://pypi.org/) and search for your package name.
     2. If the name is already taken, choose a different name and update your `pyproject.toml` file:
        ```toml
        [project]
        name = "your-new-package-name"
        ```
     3. Re-run the Copier template to update the project configuration if necessary.

### Optional: Test PyPI API Token
   - If you want to test your package uploads on [Test PyPI](https://test.pypi.org/), create a separate API token for Test PyPI.
   - Follow the same steps as for the PyPI API token, but use the **Test PyPI** website.
   - Add the token as a secret named `TEST_PYPI_API_TOKEN`.


## Standard Operating Procedure (SOP) for Releasing a Python Package

Follow these steps to release a new version of your Python package using this template:

### 1. Prepare for Release

- Ensure all changes are committed and pushed to the `main` branch.
- Verify that all tests pass and the documentation builds successfully.

### 2. Bump the Version

- Run the **Manual Version Bump** workflow:
  1. Go to the **Actions** tab in your GitHub repository.
  2. Select the **Manual version bump and push tag** workflow.
  3. Click **Run workflow** and choose the version bump type (`patch`, `minor`, or `major`).

  This workflow will:
    - Bump the version in `pyproject.toml` and `__init__.py`.
    - Create a new Git tag for the release.
    - Push the changes and tag to the `main` branch.

### 3. Trigger the Release Workflow

- The **Manual Version Bump** workflow will automatically trigger the **Release** workflow.
- The **Release** workflow will:
  - Build the package and publish it to PyPI.
  - Create a GitHub release with the new version tag.
  - Upload the built package as release assets.

### 4. Verify the Release

- Check the **Releases** tab in your GitHub repository to confirm the new release.
- Verify that the package is published on PyPI.

### 5. Update Documentation

- The **Documentation** workflow will automatically deploy the updated documentation to GitHub Pages.
- Verify the documentation is updated at `https://<your-username>.github.io/<your-repo-name>/`.

## Workflows Overview

This template includes the following GitHub Actions workflows:

### CI Workflow

- Runs tests and linting on every push and pull request.
- Ensures code quality and functionality.

### Manual Version Bump Workflow

- Allows you to manually bump the version (`patch`, `minor`, or `major`).
- Creates a new Git tag and triggers the release workflow.

### Release Workflow

- Builds the package and publishes it to PyPI.
- Creates a GitHub release and uploads release assets.

### Documentation Workflow

- Builds the documentation using Sphinx.
- Deploys the documentation to GitHub Pages on every push to `main`.


## Customizing the Template

### Adding New Features
- Add new workflows to `.github/workflows/`.
- Update the `copier.yml` file to include new prompts for customization.

### Modifying Documentation
- Edit the files in `docs/source/` to customize the documentation.
- Update the `conf.py` file to configure Sphinx.

### Adding Dependencies
- Add new dependencies to `requirements.txt` or `pyproject.toml`.

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvements, please open an issue or submit a pull request.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

## Acknowledgments

- [Copier](https://copier.readthedocs.io/) for providing an excellent templating tool.
- [GitHub Actions](https://github.com/features/actions) for enabling seamless CI/CD.
- [Sphinx](https://www.sphinx-doc.org/) for making documentation easy.





