# UVI Project Intelligence

## Environment Setup

The following steps must be completed before any coding:

1. Verify toolchain versions:
   - Python: 3.13.2 or compatible
   - UV: 0.7.2 or later (`uv --version`)
   - Ruff: 0.11.9 or later (`ruff --version`) - includes Pylint-equivalent rules
   - MyPy: latest (`mypy --version`)
   - Pre-commit: latest (`pre-commit --version`)

## UV Commands

- Check the latest available version of a specific package:

  ```bash
  uv tree --package <package> --outdated
  ```

  Example: `uv tree --package ruff --outdated`

- Check all outdated packages in the project:

  ```bash
  uv tree --outdated
  ```

- Install dependencies:

  - Run `uv sync` to install all project dependencies
  - Verify with `pytest -v` that tests pass

- Set up development environment:
  - Install pre-commit hooks: `pre-commit install`
  - Ensure git is configured with user name and email

## Code Style Patterns

- Always include `from __future__ import annotations` as the first import
- Use type annotations for function parameters and return types
- Follow PEP 8 conventions with a line length of 120 characters
- Group imports: stdlib first, third-party second, local modules third
- Use descriptive variable names and document complex logic
- NEVER use emojis in any code, documentation, or comments
- Use checkbox format `- [x]` for completed items and `- [ ]` for incomplete items

## Project-Specific Patterns

- The main CLI entry point is in `uvi/cli.py`
- Template configuration is defined in `cookiecutter.json`
- The project uses a template directory structure with `velum/`
- Generation hooks are in the `hooks/` directory
- Error handling should always provide clear, user-friendly messages

## Implementation Approaches

- When extending the CLI, modify `uvi/cli.py` directly
- For template changes, update the files in `velum/`
- For changes to the generation process, modify the hook scripts
- Always maintain backward compatibility with existing commands

## Error Handling

- Command-line tool errors should be caught and displayed clearly
- Use error codes for systematic error handling
- Provide actionable error messages that guide the user
- Handle edge cases for missing dependencies or configuration

## Feature Implementation Workflow

1. **Document Baseline Behavior**

   - Create an example project with the current code before any changes
   - Document the current user experience with specific observations
   - Save artifacts for comparison (screenshots, output logs)

2. **Implement Changes**

   - Make code modifications with appropriate error handling
   - Run linting and static analysis (ruff, mypy)
   - Run test suite to verify unit/integration tests pass

3. **Verify Implementation**

   - ALWAYS execute the actual code with the new changes
   - Create example projects to verify the feature works as expected
   - Compare with baseline to confirm correct behavior changes
   - Test edge cases (missing git, invalid config, etc.)

4. **Only Then Document**

   - Update documentation ONLY after verified working implementation
   - Include specific examples of the feature in action
   - Document both successful paths and error handling

5. **A/B Comparison**
   - Always maintain ability to compare original vs new behavior
   - Consider using git stash/branches to preserve original state
   - Provide concrete evidence of feature improvement

## Direct Testing Instructions

- Test the current codebase with UV directly:

  ```bash
  uv run python -m uvi.cli --version  # Verify version number
  uv run python -m uvi.cli            # Run project creation wizard
  ```

- Validate project version parity:

  ```bash
  # Check version matches in both locations
  grep -A 1 "version" pyproject.toml
  grep "__version__" uvi/__init__.py
  ```

- Verify template dependency versions match main project:

  ```bash
  # Compare dependency versions
  diff -u pyproject.toml example-project/pyproject.toml
  ```

- Verify template functionality:

  ```bash
  cd example-project
  uv sync              # Install dependencies
  pytest               # Run tests
  ```

- Testing after changes:
  1. Create a clean test environment: `mkdir -p /tmp/uvi-test && cd /tmp/uvi-test`
  2. Run from source: `cd <project-root> && uv run python -m uvi.cli`
  3. Verify the generated project: Check version numbers, dependencies, and configuration
  4. Run basic functionality tests on the generated project

## Testing Strategy

- Use pytest for all tests
- Test the CLI by running it with different configurations
- Mock external dependencies where appropriate
- Include both positive and negative test cases
- CRUCIAL: Execute real-world examples - passing tests is NOT sufficient verification

## Markdown Style Patterns

- Never use duplicated headings
- Use a single blank line between paragraphs
- Use a single blank line between headings and paragraphs
- Use a single blank line between paragraphs and lists
- No line length restriction (unlike code files)
- Include a blank line after any heading or subheading
- Include a blank line between numbered/bulleted list items and their indented content
- For lists with sub-items, include a blank line after the parent item
- Follow a consistent heading hierarchy (# for titles, ## for sections, etc.)
- Use fenced code blocks with language specifiers (`python instead of just`)
- Ensure all files end with a blank line

## Documentation Conventions

- Document all public functions with Google-style docstrings
- Include Args and Returns sections in docstrings
- Update README.md when adding features
- Add feature documentation to the corresponding files in docs/
- Follow the Markdown Style Patterns defined above for all documentation files

## Release Process

- Update version in `uvi/__init__.py` and `pyproject.toml`
- Create a GitHub release to trigger the release workflow
- Document changes in the release notes
- Ensure all tests pass before releasing

## Post-Release Actions

- Upgrade the global installation of UVI to the latest published version:

  ```bash
  uv tool install uvi --upgrade
  ```

- Verify the installation was successful:

  ```bash
  uvi --version
  ```

## Security Considerations

- Never include hardcoded credentials
- Validate all user input
- Use secure defaults for generated projects
- Follow security best practices in generated code

## User Interaction

- Provide clear, concise prompts
- Offer sensible defaults where possible
- Give feedback on successful operations
- Handle errors gracefully with actionable messages
