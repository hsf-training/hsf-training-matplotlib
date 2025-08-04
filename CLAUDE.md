# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based training module for the HEP Software Foundation (HSF) teaching "Matplotlib for HEP". It introduces matplotlib plotting library and creates plots commonly used in High Energy Physics, including specialized HEP styling via `mplhep`.

## Common Development Commands

### Local Development
- **Serve locally**: `make serve` - Builds and serves the Jekyll site locally
- **Build site**: `make site` - Builds the site without serving
- **Clean**: `make clean` - Removes generated files and caches

### Docker Alternative
- **Docker serve**: `make docker-serve` - Uses Docker to serve the site (requires Docker)

### Repository Maintenance
- **Repository check**: `make repo-check` - Validates repository settings
- **Lesson validation**: `make lesson-check` - Validates lesson Markdown files
- **Complete validation**: `make lesson-check-all` - Full validation including line lengths and whitespace
- **Unit tests**: `make unittest` - Runs tests on checking tools

### Pre-commit Hooks
This repository uses pre-commit hooks for code quality:
```bash
pip3 install pre-commit
pre-commit install
```

## Site Architecture

### Jekyll Structure
- **_config.yml**: Main Jekyll configuration for HSF training theme
- **_episodes/**: Lesson content in Markdown format (7 episodes total)
- **_extras/**: Additional pages (about, discussion, figures, guide)
- **_includes/**: Reusable template components
- **fig/**: Image assets for lessons
- **Gemfile**: Ruby dependencies including hsf-training-theme

### Content Organization
- Episodes are numbered sequentially (01-07) covering:
  - Introduction to Matplotlib
  - Coffee breaks (interactive elements)
  - Physics background and applications
  - Higgs search analysis
  - mplhep library usage
  - Dimuon spectrum analysis
- Uses Carpentries lesson template structure
- Physics-focused content with LaTeX math support

### Build System
- Uses Jekyll with HSF training theme
- Ruby-based build system via Bundler
- Makefile provides convenience commands
- GitHub Pages deployment via gh-pages branch
- Pre-commit hooks enforce markdown and code formatting

## Development Notes

- Main development branch: `gh-pages`
- Uses HSF training theme from remote repository
- Includes physics equation rendering via MathJax
- Associated notebooks repository for interactive content
- Binder integration for live coding sessions