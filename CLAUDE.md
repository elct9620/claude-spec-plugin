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

- **Plugin manifest** (`.claude-plugin/plugin.json`): Defines plugin identity (`name`, `version`). The `name` field becomes the skill namespace — e.g., `"name": "spec"` means skills are referenced as `spec:spec-principles`.
- **Skills** (`skills/*/SKILL.md`): Knowledge base — loaded via `Skill(spec:skill-name)` in commands.
- **Commands** (`commands/*.md`): Process orchestration — activate skills listed in `allowed-tools` frontmatter.

### Skill Format

Skills use YAML frontmatter (only `name` and `description` are required) followed by markdown content:

```yaml
---
name: skill-name
description: Brief description for skill matching
---
# Skill content in markdown
```

Skill content typically includes: **Applicability Rubric** (when to apply), **Core Principles** (the knowledge), and **Completion Rubric** (before/during/after checks).

### Command Format

Commands use an XML-based DSL to define reusable functions and a main procedure:

```xml
<function name="step-name">
    <description>What this function does.</description>
    <parameter name="param" type="string" required="true"/>
    <step>1. do something</step>
    <condition if="some condition">
        <step>2. conditional step</step>
    </condition>
    <loop for="item in $list">
        <step>3. repeated step</step>
    </loop>
    <return>what this function returns</return>
</function>

<procedure name="main">
    <step>1. <execute name="step-name" param="$value"/></step>
    <return>final output</return>
</procedure>
```

The `<execute name="main">$ARGUMENTS</execute>` at the bottom is the entry point.

## Development Guidelines

### Version Bumping

Versioning is automated via **release-please** (`.github/workflows/release-please.yml`). Merging to `main` with conventional commits triggers a release PR that auto-updates `.claude-plugin/plugin.json`.

- `fix:` commits → patch bump
- `feat:` commits → minor bump

### Skills Directory

Changes to the `skills/` and `commands/` directories are feature/fix changes, not documentation updates. Treat SKILL.md and command files as functional code, not docs.
