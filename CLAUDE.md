# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin that provides a specification knowledge agent skill (`spec-knowledge`) for creating and managing specification documents. The plugin helps AI agents maintain consistency when working with SPEC.md files and other specification documents.

## Project Structure

```
.claude-plugin/
  plugin.json       # Plugin metadata (name, version, description)
skills/
  spec-knowledge/
    SKILL.md        # Skill definition with specification expertise
```

## Plugin Architecture

- **Plugin manifest** (`.claude-plugin/plugin.json`): Defines plugin identity and metadata
- **Skills** (`skills/*/SKILL.md`): Markdown files with YAML frontmatter that define agent skills

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

Changes to the `skills/` directory are feature/fix changes, not documentation updates. Treat SKILL.md files as functional code, not docs.
