# Copilot instructions for the Clash ruleset repository

## Project context

This repository stores Clash/Mihomo ruleset assets and documentation. Most changes are to rule lists, example YAML snippets, or README content rather than code.

## Repository map

- Root README files: [README.md](../README.md) and [README_EN.md](../README_EN.md)
- Location-based rules: [The_Location_rule-set/README.md](../The_Location_rule-set/README.md) and [The_Location_rule-set/README_EN.md](../The_Location_rule-set/README_EN.md)
- Rule files: [The_Location_rule-set/](../The_Location_rule-set/)
- Generated Adobe assets: [other/adobe/block/](../other/adobe/block/)
- Automation workflow: [.github/workflows/adobe-ruleset.yml](workflows/adobe-ruleset.yml)

## Working expectations

- Keep file names and directory structure intact unless a change genuinely requires a rename.
- Preserve the repository’s bilingual documentation approach: update Chinese and English docs together when behavior or coverage changes.
- Follow the existing formatting for rule lists and example YAML snippets.
- Prefer minimal, targeted changes and avoid introducing new tooling or build steps.
- If a rule file is added or renamed, ensure references in the README files are updated accordingly.
