# velum

[![Release](https://img.shields.io/github/v/release/shaneholloman/velum)](https://img.shields.io/github/v/release/shaneholloman/velum)
[![Build status](https://img.shields.io/github/actions/workflow/status/shaneholloman/velum/main.yml?branch=main)](https://github.com/shaneholloman/velum/actions/workflows/main.yml?query=branch%3Amain)
[![Commit activity](https://img.shields.io/github/commit-activity/m/shaneholloman/velum)](https://img.shields.io/github/commit-activity/m/shaneholloman/velum)
[![License](https://img.shields.io/github/license/shaneholloman/velum)](https://img.shields.io/github/license/shaneholloman/velum)

A Python project template with a focus on simplicity and ease of use. It includes a CI/CD pipeline, pre-commit hooks, and a set of tools to help you get started quickly.

## Purpose of This Template

This repository serves two purposes:

1. **Project Template**: The primary purpose is to provide a complete, ready-to-use project structure for Python applications with best practices already configured.

2. **Pipeline Demonstration**: The included minimal package demonstrates that the CI/CD pipeline, documentation, and publishing workflows function correctly.

When published to PyPI, the template itself becomes a minimal package. You should replace this placeholder code with your actual application while keeping the project structure.

## Getting Started

### Creating a New Repository from this Template

This repository is set up as a GitHub template. To use it:

1. Click the "Use this template" button at the top of the repository page
2. Name your new repository
3. Clone your newly created repository

The included sample application (`velum`) is a proof of concept that demonstrates the pipeline functionality. Simply replace it with your own application code while keeping the project structure, and the CI/CD pipeline will work seamlessly.

### Development Setup

1. **IMPORTANT: First Required Step After Cloning**

   Always run the following command immediately after cloning this template:

   ```sh
   make install
   ```

   This critical step:

   - Installs the virtual environment with `uv sync`
   - Sets up pre-commit hooks that automatically fix formatting issues when committing
   - Generates your `uv.lock` file

   Without this step, pre-commit hooks won't run automatically when committing via terminal or VSCode.

2. Run the pre-commit hooks to resolve potential formatting issues:

   ```sh
   uv run pre-commit run -a
   ```

3. Commit the changes:

   ```sh
   git add .
   git commit -m 'Fix formatting issues'
   git push origin main
   ```

## Setting up PyPI Publishing

To publish your package to PyPI:

1. Create an API Token on [PyPI](https://pypi.org/)
2. Add the token to your repository using the GitHub CLI:

   ```sh
   gh secret set PYPI_TOKEN -b "your-pypi-token-here"
   ```

3. When creating a release on GitHub, the workflow will automatically publish your package to PyPI

## Setting up GitHub Pages Documentation

To enable automatic documentation deployment:

1. Go to your repository's Settings → Pages
2. Under "Build and deployment":

   - Set "Source" to "Deploy from a branch"
   - Set "Branch" to "gh-pages"
   - Set "Directory" to "/" (root)
   - Click "Save"

   > **Important:** Do not select the "docs" directory as the source - the deployment workflow is configured to use the root directory of the gh-pages branch.

### Working with Documentation Locally

You can preview the documentation locally by running:

```sh
uv run mkdocs serve
```

This will start a local server at <http://127.0.0.1:8000/> where you can preview your documentation as you work on it.

## Releasing a New Version

- Create an API Token on [PyPI](https://pypi.org/) if you haven't already
- Add the API Token to your project's secrets with the name `PYPI_TOKEN`
- Create a new release on GitHub using the GitHub CLI:

  ```sh
  gh release create 0.1.0 --title "0.1.0" --generate-notes
  ```

  This automatically creates both the release and a tag in one step.

The release workflow will automatically:

1. Update the version in your project files
2. Build the package
3. Publish to PyPI
4. Deploy updated documentation

For more details on the CI/CD process, see [here](https://shaneholloman.github.io/uvi/features/cicd/#how-to-trigger-a-release).
