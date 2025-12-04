# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains shareable [Renovate](https://docs.renovatebot.com/) configuration presets for thelab projects. Renovate is a dependency update automation tool. Projects can extend these presets to get standardized dependency update behavior.

## Available Presets

- **default.json** - Base configuration that all other presets extend. Includes common settings like timezone, range strategies, package groupings, and custom version extractors.
- **application.json** - For production applications. Pins to current LTS versions of Node, Python, Django, and Wagtail.
- **application-non-lts.json** - For applications that can use non-LTS versions. More permissive Python version constraints.
- **library.json** - For library packages. More conservative constraints on runtime dependencies.

## Commands

```bash
# Install dependencies
npm ci

# Run linting (pre-commit hooks)
pip3 install pre-commit
pre-commit run --all-files

# Format JSON files manually
npx prettier --write "*.json"
```

## How to Use These Presets

Projects reference these presets via the `extends` key in their `renovate.json`:

```json
{
    "extends": ["gitlab>thelabnyc/renovate-config:application"]
}
```

The preset name corresponds to the JSON filename (without `.json` extension).

## Key Configuration Patterns

- Package replacements are defined for deprecated packages (e.g., `typed-scss-modules` → `@thelabnyc/typed-scss-modules`)
- Custom regex managers extract versions from non-standard locations (e.g., `UV_VERSION` in YAML files)
- Docker images from `registry.gitlab.com/thelabnyc/*` use custom versioning patterns
- Related packages are grouped (eslint, boto, tox, python, node) to reduce MR noise
