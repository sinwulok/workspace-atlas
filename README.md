# workspace-atlas

A curated repository ecosystem containing research projects, development applications, and templates across multiple domains.

本 repository 採用功能分類的治理結構，將專案依性質分為 Research、Development 和 Other 三大類別。

---

## Overview

workspace-atlas is a curated collection of projects spanning data science, machine learning, frontend development, and specialized tools. Each project is categorized by its nature and maintained with consistent documentation and metadata standards.

---

## Repository Structure

```
workspace-atlas/
├── Research/              # Research projects
├── Development/           # Development projects
├── Other/                 # Templates and utilities
├── catalog/               # Project index and metadata
├── docs/                  # Governance documentation
├── .github/               # GitHub configuration and workflows
└── README.md              # This file
```

---

## Project Categories

### Research/
Research projects including data science, machine learning, forecasting models, and academic or experimental work.

- **cnogb-bond-signal-anomaly** - Bond forecasting and anomaly detection with Transformer models
- **machine-learning-applications-in-fmri** - Machine learning applications for fMRI analysis
- **e-learning-fa-ipy** - E-learning data analysis with Jupyter notebooks

### Development/
Development projects including frontend applications, trading signal detection, neural networks, and production applications.

- **amc-amr-gff-nn** - AMC AMR Gated Fusion Former neural network project
- **animated-gradient-text-starter** - Animated gradient text starter (Next.js + TypeScript + Tailwind)
- **r3f-portfolio** - React Three Fiber 3D portfolio website
- **binance-multi-assets-singal-agent** - Binance multi-asset trading signal agent prototype

### Other/
Templates, tools, and utilities for general-purpose use.

- **sw-single-page-cv-latex-templates** - LaTeX single-page CV templates

---

## Catalog

For complete project listings, metadata, and tag information, see:
- **Machine-readable**: [catalog/projects.yml](catalog/projects.yml)
- **Human-readable**: [catalog/index.md](catalog/index.md)

---

## Governance

Repository governance documentation is located in the `docs/` directory:

- [Architecture](docs/architecture.md) - Repository architecture and directory purpose
- [Migration Plan](docs/migration-plan.md) - Detailed refactoring history
- [Naming Conventions](docs/naming-conventions.md) - Project and file naming standards
- [Project Lifecycle](docs/project-lifecycle.md) - Project status management
- [Governance](docs/governance.md) - Repository governance principles
- [Branch Policy](docs/branch-policy.md) - Branch management and development workflow

---

## How to Find a Project

Browse projects by:
1. **Category**: Navigate to `Research/`, `Development/`, or `Other/` directories
2. **Tags**: Check [catalog/tags.yml](catalog/tags.yml) for topic-based filtering
3. **Lifecycle**: See [catalog/statuses.yml](catalog/statuses.yml) for project maturity levels

---

## How to Download a Single Project

If you only need a specific subfolder from this monorepo, here are convenient methods to avoid downloading the entire repository.

### Method 1: Git sparse-checkout (Recommended)

Best for users who need git functionality but only want specific folders.

```bash
# Clone with minimal blobs and enable sparse mode
git clone --filter=blob:none --sparse https://github.com/sinwulok/workspace-atlas.git
cd workspace-atlas

# Fetch only the folder you need (example)
git sparse-checkout set Research/cnogb-bond-signal-anomaly

# Optionally checkout another branch
git checkout <branch>
```

### Method 2: SVN export (Quick, no git)

Suitable for public GitHub repos, returns a plain folder without .git.

```bash
svn export https://github.com/sinwulok/workspace-atlas/trunk/Research/cnogb-bond-signal-anomaly
```

### Method 3: Download ZIP and extract specific folder

Download a snapshot of the entire repository (larger), then extract only the needed folder.

```bash
curl -L -o repo.zip https://github.com/sinwulok/workspace-atlas/archive/refs/heads/<branch>.zip
unzip repo.zip "workspace-atlas-<branch>/Research/cnogb-bond-signal-anomaly/*" -d extracted
```

Replace `<branch>` with the branch name (e.g., `main`).

### Method 4: GitHub CLI

If using the `gh` CLI:

```bash
gh repo clone sinwulok/workspace-atlas -- --filter=blob:none --sparse
cd workspace-atlas
git sparse-checkout set Research/cnogb-bond-signal-anomaly
```

---

## Notes

- Private repositories require SSH or HTTPS authentication
- `svn export` works for public repos; private repos require authentication
- If you need full git history, avoid using `--depth 1` and `--filter=blob:none`
- sparse-checkout is recommended for contributors who need git functionality

---

## Contributing

Contributions are welcome. Please follow the repository governance guidelines and naming conventions when submitting changes.

---

## License

See individual projects for specific licensing information.
