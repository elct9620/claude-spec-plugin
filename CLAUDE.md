# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin that provides specification knowledge and commands for creating and managing specification documents. Skills provide domain knowledge; commands orchestrate workflows that reference those skills.

## Project Structure

```
.claude-plugin/
  plugin.json           # Plugin metadata (name, version, description)
skills/
  spec-principles/
    SKILL.md            # Core principles — what a spec IS/IS NOT, anti-patterns
  spec-framework/
    SKILL.md            # Three-layer framework — Intent, Design, Consistency
  spec-quality/
    SKILL.md            # Quality criteria — rubric, balance check, common problems
  spec-methodology/
    SKILL.md            # Methods — progressive approach, reviewing, splitting, uncertainty
commands/
  spec-write.md         # Write or improve specifications
  spec-review.md        # Review specifications against quality criteria
```

## Plugin Architecture

- **Plugin manifest** (`.claude-plugin/plugin.json`): Defines plugin identity and metadata
- **Skills** (`skills/*/SKILL.md`): Knowledge base — markdown files with YAML frontmatter that define agent skills
- **Commands** (`commands/*.md`): Process orchestration — procedural workflows that reference skills via `Skill()` in `allowed-tools`

### Skill Format

Skills use YAML frontmatter for metadata followed by markdown content:
```yaml
---
name: skill-name
description: Brief description for skill matching
license: Apache-2.0
metadata:
  author: Author Name
---
# Skill content in markdown
```

## Development Guidelines

### Version Bumping

- Use `fix:` commits for patch version bumps
- Use `feat:` commits for minor version bumps
- Update version in `.claude-plugin/plugin.json`

### Skills Directory

Changes to the `skills/` and `commands/` directories are feature/fix changes, not documentation updates. Treat SKILL.md and command files as functional code, not docs.
