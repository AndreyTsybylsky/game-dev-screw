# Contributing to game-dev-screw

This is a personal fork of [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios), adapted for **VS Code + GitHub Copilot**.

## Repository

**Remote**: `https://github.com/AndreyTsybylsky/game-dev-screw`

## Branch Structure

| Branch | Purpose |
|--------|---------|
| `main` | Upstream source (original Claude Code framework) |
| `copilot-adaptation` | VS Code / GitHub Copilot adaptation — active development branch |

## What Was Added (`copilot-adaptation`)

The `.github/` directory maps Claude Code concepts to VS Code Copilot equivalents:

| Claude Code | VS Code Copilot | Location |
|---|---|---|
| `CLAUDE.md` | Global instructions | `.github/copilot-instructions.md` |
| `.claude/rules/*.md` | Scoped instructions | `.github/instructions/*.instructions.md` |
| `.claude/agents/*.md` | Custom agent modes | `.github/agents/*.agent.md` |
| `.claude/skills/*/SKILL.md` | Reusable prompts | `.github/prompts/*.prompt.md` |

The original `.claude/` folder is preserved for parallel Claude Code use.

## Local Setup

```bash
git clone https://github.com/AndreyTsybylsky/game-dev-screw.git
cd game-dev-screw
git checkout copilot-adaptation
```

## Pushing Changes

### First-time setup (generate a PAT with `repo` scope at github.com/settings/tokens):

```bash
git remote set-url origin https://<YOUR_TOKEN>@github.com/AndreyTsybylsky/game-dev-screw.git
```

### Push to the active branch:

```bash
git add .
git commit -m "your message"
git push origin copilot-adaptation
```

### Open a PR from `copilot-adaptation` → `main`:

```
https://github.com/AndreyTsybylsky/game-dev-screw/pull/new/copilot-adaptation
```

## Syncing with Upstream

```bash
git remote add upstream https://github.com/Donchitos/Claude-Code-Game-Studios.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

Then rebase `copilot-adaptation` onto the updated `main`:

```bash
git checkout copilot-adaptation
git rebase main
git push origin copilot-adaptation --force-with-lease
```
