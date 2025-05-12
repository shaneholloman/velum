# MkDocs YAML Special Syntax Preservation

## Brief overview

These guidelines cover the proper handling of specific YAML syntax in MkDocs configuration files. Certain YAML syntax patterns that may appear as errors or unresolved tags in editors are actually required for proper MkDocs functionality with Material theme extensions. AI assistants must never attempt to "fix" or modify these special syntax patterns.

## Critical Python Tags

- The `!!python/name:` and `!!python/object/apply:` tags in mkdocs.yml are essential for proper functioning of the MkDocs Material theme extensions
- Despite appearing as "unresolved tags" in many editors and linters, these tags MUST be preserved exactly as written
- Never attempt to replace these tags with string equivalents or other YAML syntax
- These tags allow Python function/class references within the YAML configuration

## Preservation Examples

- Always preserve the exact syntax of the following configurations:

```yaml
# For mermaid diagrams - preserve exactly as shown
pymdownx.superfences:
  custom_fences:
    - name: mermaid
      class: mermaid
      format:
        !!python/name:pymdownx.superfences.fence_code_format # For tabbed interfaces - preserve exactly as shown


pymdownx.tabbed:
  alternate_style: true
  combine_header_slug: true
  slugify: !!python/object/apply:pymdownx.slugs.slugify
    kwds:
      case: lower
```

## Warning Signs

- If you notice any of the following in mkdocs.yml configuration, do NOT modify them:
  - Any tag starting with `!!python/`
  - Specifically `!!python/name:` and `!!python/object/apply:` tags
  - Any unusual indentation patterns associated with these tags
  - The exact spacing and formatting around these tags

## Acceptable Modifications

- You MAY modify other aspects of the mkdocs.yml file such as:
  - Site name, description, URL, etc.
  - Navigation structure
  - Adding new plugins or extensions
  - Changing theme colors or features
  - Any other configuration that does not involve the special Python tags

## Error Handling

- If you encounter errors related to these special tags, do not attempt to "fix" the syntax
- Instead, investigate other potential issues such as:
  - Missing Python dependencies
  - MkDocs version compatibility
  - Plugin installation issues
  - Other configuration errors unrelated to the special syntax
