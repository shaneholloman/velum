# GitHub Actions Caching Strategy

## Brief overview

These guidelines cover best practices for implementing reliable caching in GitHub Actions workflows when using matrix strategies with UV package manager. They address common issues like 422 cache failures and provide a standardized approach to caching dependencies efficiently.

## UV Tool Caching

- Always disable the built-in caching mechanism in the `astral-sh/setup-uv` action by setting `enable-cache: "false"`
- Implement manual caching for UV dependencies using GitHub's native cache action
- UV dependencies should be cached at `~/.cache/uv` path
- Create separate caches for different Python versions in matrix jobs

## Matrix Strategy Configuration

- When using matrix strategies for multi-version testing, include the matrix version in the cache key
- Example cache key pattern: `uv-${{ matrix.python-version }}-${{ hashFiles('uv.lock') }}`
- For non-matrix jobs, use a fixed version in the cache key (e.g., `uv-3.12-${{ hashFiles('uv.lock') }}`)
- Include restore-keys with partial matches for better cache utilization

## Cache Implementation

- Add cache steps right after the environment setup step in each job
- Use the following template for matrix jobs:

  ```yaml
  - name: Cache UV dependencies
    uses: actions/cache@v4
    with:
      path: ~/.cache/uv
      key: uv-${{ matrix.python-version }}-${{ hashFiles('uv.lock') }}
      restore-keys: |
        uv-${{ matrix.python-version }}-
  ```

- For non-matrix jobs, use a fixed version:

  ```yaml
  - name: Cache UV dependencies
    uses: actions/cache@v4
    with:
      path: ~/.cache/uv
      key: uv-3.12-${{ hashFiles('uv.lock') }}
      restore-keys: |
        uv-3.12-
  ```

## Pre-commit Cache Configuration

- Pre-commit caches should be separate from UV dependency caches
- Use the pre-commit config file for the cache key: `pre-commit-${{ hashFiles('.pre-commit-config.yaml') }}`
- Cache pre-commit at the standard location: `~/.cache/pre-commit`

## Versioning Considerations

- Update UV version in custom actions to match the project requirements
- Follow the versioning requirements specified in the project rules
- Current project requires UV 0.5.14 or later

## Workflow Testing and Troubleshooting

- Monitor workflow runs to verify cache hits/misses are working as expected
- If 422 errors occur, check for incorrect variable usage or context availability
- When debugging cache issues, inspect the full step output in the workflow run logs
- Cache keys containing undefined variables will cause 422 errors
