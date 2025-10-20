# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based training module for the HEP Software Foundation (HSF) teaching "Matplotlib for HEP". It introduces matplotlib plotting library and creates plots commonly used in High Energy Physics, including specialized HEP styling via `mplhep`.

## Recent Updates

The training materials have been modernized to align with current matplotlib and Python best practices:
- Updated to modern matplotlib 3.x+ styling and API usage
- Enhanced with mplhep context managers and experiment-specific styles
- Fixed deprecated functions and improved plot aesthetics
- Added comprehensive requirements.txt for dependency management
- Updated MathJax to modern CDN for equation rendering

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
  - **01-introduction.md**: Matplotlib basics, modern best practices, figure creation
  - **02-coffee-break.md**: Interactive break elements
  - **03-physics.md**: Standard Model background, particle physics theory
  - **04-higgs-search.md**: Real ATLAS data analysis, histogram techniques
  - **05-mplhep.md**: HEP-specific styling, experiment themes (CMS, ATLAS, etc.)
  - **06-coffee-break.md**: Interactive break elements
  - **07-dimuonspectrum.md**: Advanced analysis with invariant mass calculations
- Uses Carpentries lesson template structure
- Physics-focused content with LaTeX math support via modern MathJax

### Build System
- Uses Jekyll with HSF training theme
- Ruby-based build system via Bundler
- Makefile provides convenience commands
- GitHub Pages deployment via gh-pages branch
- Pre-commit hooks enforce markdown and code formatting

## Development Notes

- Main development branch: `gh-pages`
- Uses HSF training theme from remote repository
- Includes physics equation rendering via modern MathJax 3.x
- Associated notebooks repository for interactive content: `hsf_matplotlib_notebooks`
- Multiple cloud platforms supported: Binder, Google Colab, GitHub Codespaces, CERN SWAN
- **requirements.txt** available for local Python environment setup

## Python Dependencies

The repository includes a comprehensive `requirements.txt` with:
- Core: matplotlib>=3.6.0, numpy, pandas
- HEP-specific: mplhep>=0.3.0, uproot>=4.0.0, hist>=2.6.0
- Jupyter ecosystem: jupyterlab>=4.0.0, notebook, ipywidgets
- Data handling: h5py for HDF5 files

## Code Style Guidelines

- Use explicit `fig, ax = plt.subplots()` pattern
- Prefer `plt.show()` over `fig.show()`
- Use context managers for temporary styling: `with hep.style.use("CMS"):`
- Include `plt.tight_layout()` for better subplot spacing
- Add subtle grids with `alpha=0.3` for better readability
- Use modern error bar styling with `capsize` and `markersize` parameters