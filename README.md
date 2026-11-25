> [!NOTE]
> **This skill lives in the main collection: [milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills/tree/main/skills/pre-commit-setup)**. Please ⭐ star it there; that's where updates land first.
> Docs: **https://milad-ahmd.github.io/agent-skills/skills/pre-commit-setup/** · Claude Code: `/plugin install all-skills --marketplace milad-ahmd/agent-skills`

<div align="center">

# 🚦 pre-commit-setup

**Fast git hooks from the tools you already use: pre-commit, husky + lint-staged or lefthook, mirrored in CI. An Agent Skill for Claude Code, Cline, Cursor, Codex and other AI coding agents.**

[![License: MIT](https://img.shields.io/github/license/milad-ahmd/pre-commit-setup)](LICENSE)
[![Stars](https://img.shields.io/github/stars/milad-ahmd/pre-commit-setup?style=social)](https://github.com/milad-ahmd/pre-commit-setup)
![Category](https://img.shields.io/badge/category-Git%20%26%20Workflow-blue)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cline%20%7C%20Cursor%20%7C%20Codex-8A2BE2)

[Install](#-install) · [Usage](#-usage) · [How it works](skills/pre-commit-setup/SKILL.md) · [All skills](https://github.com/milad-ahmd/agent-skills)

</div>

> Part of **[agent-skills](https://github.com/milad-ahmd/agent-skills)**, a growing collection of practical skills for AI coding agents.

## 📦 Install

**One command (installs the whole collection):**

```bash
curl -fsSL https://raw.githubusercontent.com/milad-ahmd/agent-skills/main/install.sh | bash -s -- pre-commit-setup
```

**Manually (Claude Code):**

```bash
git clone https://github.com/milad-ahmd/pre-commit-setup /tmp/pre-commit-setup
mkdir -p ~/.claude/skills && cp -r /tmp/pre-commit-setup/skills/pre-commit-setup ~/.claude/skills/
```

**Per project:** copy `skills/pre-commit-setup` into `<project>/.claude/skills/`.
**Any other agent:** paste [`SKILL.md`](skills/pre-commit-setup/SKILL.md) into your rules or system prompt.

## 💬 Usage

Just ask your agent:

```text
Set up pre-commit hooks for this repo with ruff
Add husky and lint-staged so eslint and prettier run on commit
```

The full workflow, rules and output format are in [`SKILL.md`](skills/pre-commit-setup/SKILL.md).

## 🔎 Sample output

`hooks_plan.py` is plain Python 3 with no dependencies and only reads the repo unless you pass `--write`. Real output on a small Python repo that already uses ruff:

```text
$ python3 hooks_plan.py -C my-python-repo

Stack: python (1 files)
Package managers: none
Monorepo: no

Recommended: pre-commit (Python project: pre-commit pins each hook's version and installs it in its own env)
Hooks (staged files only):
  large-files     blocks new files over 500 KB
  gitleaks        scans the staged diff for secrets
  ruff-check      [tool.ruff] in pyproject.toml
  ruff-format     [tool.ruff.format] in pyproject.toml

--- .pre-commit-config.yaml ---
# Git hooks for this repo. Install: pre-commit install. Update revs: pre-commit autoupdate
# Skip one hook: SKIP=<id> git commit ...   Skip all: git commit --no-verify (CI still runs them)
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v6.0.0
    hooks:
      - id: check-added-large-files
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.30.1
    hooks:
      - id: gitleaks
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.17.6
    hooks:
…
```

`--write` creates the config only when no hook setup exists, and never overwrites a file. Exit codes: `0` plan, `1` a hook setup already exists, `2` not a git repo.

## 🧩 More skills

See the full collection: **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 🤝 Contributing

This repo is a read-only mirror. Please open issues and PRs in **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 📄 License

[MIT](LICENSE) © Milad Ahmadi

<div align="center">

**If this skill saved you time, a ⭐ helps others find it.**

</div>
