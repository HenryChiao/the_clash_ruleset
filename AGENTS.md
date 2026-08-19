# AGENTS.md

## Repository purpose

This repository contains a collection of Mihomo/Clash rulesets for location-based routing, especially Wi-Fi Calling and banking services. The content is primarily data-driven: rule lists in plain text, example Clash/Mihomo YAML snippets, and documentation in both Chinese and English.

## Key directories

- [README.md](README.md) and [README_EN.md](README_EN.md): project overview and usage guidance.
- [The_Location_rule-set/README.md](The_Location_rule-set/README.md) and [The_Location_rule-set/README_EN.md](The_Location_rule-set/README_EN.md): detailed rule-set documentation.
- [The_Location_rule-set/](The_Location_rule-set/): rule files and examples. Rule files are grouped by purpose, e.g. `wificalling-*.list`, `bank-*.list`, and `apple-location.list`.
- [other/adobe/block/](other/adobe/block/): generated Adobe-related ruleset assets.
- [.github/workflows/](.github/workflows/): automation workflows, especially [adobe-ruleset.yml](.github/workflows/adobe-ruleset.yml).

## Working conventions

- Preserve the existing structure and naming patterns. Do not rename rule files casually because other docs and examples may reference them.
- Prefer small, targeted edits. These files are mostly rules and documentation rather than application code.
- When adding or changing rule sets, update the relevant documentation in both Chinese and English READMEs when the change affects usage or coverage.
- Keep comments and examples consistent with the repository’s existing style. The project uses clear, explicit examples for Clash/Mihomo configuration.
- For generated or workflow-related changes, be careful not to break the automation flow in [.github/workflows/adobe-ruleset.yml](.github/workflows/adobe-ruleset.yml).

## Editing guidance

- Rule lists should stay plain text and follow the repository’s existing format.
- If a new category or file is introduced, add it to the appropriate README table or section so the docs remain aligned with the actual files.
- Example YAML files should remain illustrative and should not introduce unrelated tooling or dependencies.

## Verification

There is no application build/test pipeline for this repository. Before concluding a change:

- confirm the affected file paths and names are correct;
- ensure any referenced filenames still match the actual files in the repository;
- review the Markdown/YAML content for obvious formatting and consistency issues.
