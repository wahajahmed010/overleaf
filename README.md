# overleaf-latex

![ClawHub](https://img.shields.io/badge/clawhub-v1.1.0-blue) ![License](https://img.shields.io/badge/license-MIT--0-green) ![Type](https://img.shields.io/badge/type-OpenClaw%20Skill-orange)

An OpenClaw skill for managing Overleaf LaTeX projects via git integration. Clone projects, create branches for tailored versions, edit LaTeX, compile locally, and push back — all driven by agent instructions.

Published on [ClawHub](https://clawhub.ai/skills/overleaf-latex). Companion plugin: [wahajahmed010/openclaw-overleaf](https://github.com/wahajahmed010/openclaw-overleaf).

## Features

- **Git-based workflow** — Clone, branch, and push Overleaf projects using standard git commands
- **Local compilation** — Verify LaTeX compiles before pushing to avoid broken documents on Overleaf
- **Resume versioning** — One branch per company or role, keeping the base resume clean
- **Health checking** — Verify Overleaf credentials, git connectivity, and LaTeX compiler availability
- **Common patterns** — Reference guide for frequent LaTeX resume edits (tailoring sections, reordering, adjusting spacing)
- **Error handling** — Guidance for authentication failures, merge conflicts, compilation errors

## Installation

Install from ClawHub:

```bash
clawhub install overleaf-latex
```

## Quick Start

### 1. Store Overleaf credentials

```bash
echo "OVERLEAF_EMAIL=your@email.com" > ~/.openclaw/.overleaf_credentials
echo "OVERLEAF_PASSWORD=your_password_or_token" >> ~/.openclaw/.overleaf_credentials
chmod 600 ~/.openclaw/.overleaf_credentials
```

### 2. Install LaTeX (if not already installed)

```bash
# Ubuntu/Debian
sudo apt-get install -y texlive-latex-base texlive-latex-extra texlive-fonts-recommended

# macOS
brew install --cask mactex

# Verify
which pdflatex && pdflatex --version
```

### 3. Clone and work on a project

```bash
# Clone your Overleaf project
git clone https://git.overleaf.com/<project-id> my-resume
cd my-resume

# Create a tailored version
git checkout -b resume/company-slug

# Edit the .tex files, then compile
pdflatex -interaction=nonstopmode main.tex

# Push back to Overleaf
git add -A && git commit -m "tailor: resume for Company" && git push origin resume/company-slug
```

## What's Included

| File | Purpose |
|------|---------|
| `SKILL.md` | Skill instructions, workflow, prerequisites, and error handling |
| `scripts/overleaf_health.py` | Health check script — verifies credentials, git connectivity, and LaTeX compiler |
| `references/latex-patterns.md` | Common LaTeX resume edit patterns and commands |

## Health Check

Run the health check to verify the entire Overleaf integration:

```bash
python3 scripts/overleaf_health.py
```

This checks:

- Overleaf credentials are stored and readable
- Git can reach `git.overleaf.com`
- `pdflatex` is available in PATH
- A test LaTeX compilation succeeds

Run this after initial setup and any time you encounter connectivity or compilation issues.

## Constraints

- **Never push without local compilation** — always run `pdflatex` (or your configured compiler) before pushing to Overleaf
- **Never force push to master** — the base resume must stay intact
- **One branch per company** — don't mix tailored versions on the same branch
- **Pull before push** — Overleaf web edits can diverge from your local clone; pull first to avoid conflicts
- **Keep credentials at `~/.openclaw/.overleaf_credentials`** with `chmod 600` — never log or print credential values

## Using with the Plugin

For native agent tool integration (6 tools: `overleaf_clone`, `overleaf_branch`, `overleaf_compile`, `overleaf_push`, `overleaf_status`, `overleaf_health`), install the companion plugin:

```bash
openclaw plugins install clawhub:@wahajahmed010/openclaw-overleaf
```

The plugin provides the same workflow as first-class agent tools, so you don't need to run git commands manually. The skill covers the manual workflow; the plugin automates it.

## Links

- **ClawHub skill page:** https://clawhub.ai/skills/overleaf-latex
- **Companion plugin repo:** https://github.com/wahajahmed010/openclaw-overleaf
- **ClawHub plugin page:** https://clawhub.ai/plugins/@wahajahmed010/openclaw-overleaf

## License

MIT-0