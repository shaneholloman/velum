# velum

[![Build status](https://img.shields.io/github/actions/workflow/status/shaneholloman/velum/main.yml?branch=main)](https://github.com/shaneholloman/velum/actions/workflows/main.yml?query=branch%3Amain)
[![validate-codecov-config](https://github.com/shaneholloman/velum/actions/workflows/validate-codecov-config.yml/badge.svg)](https://github.com/shaneholloman/velum/actions/workflows/validate-codecov-config.yml)
[![Commit activity](https://img.shields.io/github/commit-activity/m/shaneholloman/velum)](https://img.shields.io/github/commit-activity/m/shaneholloman/velum)

A Python project template with a focus on simplicity and ease of use. It includes a CI/CD pipeline, pre-commit hooks, and a set of tools to help you get started quickly.

- **Github repository**: <https://github.com/shaneholloman/velum/>
- **Documentation**: <https://shaneholloman.github.io/velum/>

## Purpose of This Template

This repository serves two purposes:

1. **Project Template**: The primary purpose is to provide a complete, ready-to-use project structure for Python applications with best practices already configured.

2. **Pipeline Demonstration**: The included minimal package demonstrates that the CI/CD pipeline, documentation, and publishing workflows function correctly.

When published to PyPI, the template itself becomes a minimal package. You should replace this placeholder code with your actual application while keeping the project structure.

## Getting started with your project

### 1. Create a New Repository from this Template

This repository is set up as a GitHub template. To use it:

1. Click the "Use this template" button at the top of the repository page
2. Name your new repository
3. Clone your newly created repository

The included sample application (`velum`) is a proof of concept that demonstrates the pipeline functionality. Simply replace it with your own application code while keeping the project structure, and the CI/CD pipeline will work seamlessly.

### 2. Set Up Your Development Environment

Install the environment and the pre-commit hooks with:

```sh
make install
```

This will also generate your `uv.lock` file.

### 3. Run the pre-commit hooks

Initially, the CI/CD pipeline might be failing due to formatting issues. To resolve those run:

```sh
uv run pre-commit run -a
```

### 4. Commit the changes

Lastly, commit the changes made by the two steps above to your repository.

```sh
git add .
git commit -m 'Fix formatting issues'
git push origin main
```

You are now ready to start development on your project!
The CI/CD pipeline will be triggered when you open a pull request, merge to main, or when you create a new release.

## Setting up PyPI Publishing

To publish your package to PyPI:

1. Create an API Token on [PyPI](https://pypi.org/)
2. Add the token to your repository using the GitHub CLI:

   ```sh
   gh secret set PYPI_TOKEN -b "your-pypi-token-here"
   ```

   Alternatively, add it manually in your repository's Settings → Secrets → Actions → New repository secret
3. When creating a new release on GitHub, the workflow will automatically publish your package to PyPI

## Setting up GitHub Pages Documentation

To enable automatic documentation deployment:

1. Go to your repository's Settings → Pages
2. Under "Build and deployment":
   - Set "Source" to "Deploy from a branch"
   - Set "Branch" to "gh-pages"
   - Set "Directory" to "/" (root)
   - Click "Save"

   > **Important:** Do not select the "docs" directory as the source - the deployment workflow is configured to use the root directory of the gh-pages branch.

After setting this up and pushing changes to main, your documentation will be automatically deployed to `https://[username].github.io/[repository-name]/`

### Working with Documentation Locally

You can preview the documentation locally by running:

```sh
uv run mkdocs serve
```

This will start a local server at http://127.0.0.1:8000/ where you can preview your documentation as you work on it.

## Releasing a new version

- Create an API Token on [PyPI](https://pypi.org/) if you haven't already
- Add the API Token to your project's secrets with the name `PYPI_TOKEN` using:

  ```sh
  gh secret set PYPI_TOKEN -b "your-pypi-token-here"
  ```

- Create a new release on GitHub using the GitHub CLI:

  ```sh
  gh release create 0.1.0 --title "0.1.0" --generate-notes
  ```

  This automatically creates both the release and a tag in one step.

  Alternatively, you can [create a release manually](https://github.com/shaneholloman/velum/releases/new) through the GitHub web interface.

The release workflow will automatically:

1. Update the version in your project files
2. Build the package
3. Publish to PyPI
4. Deploy updated documentation

For more details, see [here](https://shaneholloman.github.io/uvi/features/cicd/#how-to-trigger-a-release).

## Additional configuration options

To enable code coverage reports, see [here](https://shaneholloman.github.io/uvi/features/codecov/).

---

Repository initiated with [shaneholloman/uvi](https://github.com/shaneholloman/uvi).
