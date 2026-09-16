# Contributing to jorgo-ai-framework

This is a personal fork, maintained solo by [Jorgo69](https://github.com/Jorgo69). No issue-triage team, no "Certified Member" roles, no separate `next` branch — one branch (`main`), protected, changed only through pull requests.

## 🔀 The only path: branch → PR → merge

`main` is protected on GitHub: **no direct push, not even for the owner**. Every change, including a one-line fix, goes through this flow:

```bash
# 1. Branch off main
git checkout main && git pull
git checkout -b fix/short-description     # or feat/, docs/, chore/...

# 2. Work, commit normally
git add <files>
git commit -m "<type>(<scope>): description"   # Conventional Commits

# 3. Push the branch (never main directly — GitHub will refuse it anyway)
git push -u origin fix/short-description

# 4. Open the PR
gh pr create --fill

# 5. Merge it yourself once you're satisfied — no external approval is required
#    (branch protection only requires a PR to exist, not a review from someone else)
gh pr merge --squash
```

`--squash` keeps `main`'s history at one commit per PR. Use `--merge` instead if you want every commit preserved.

## 📜 Principles

- **No slop** — read every line before proposing it.
- **Spend tokens like they cost something.**
- **Claude Code syntax only** — skills, agents, and rules are authored in Claude Code syntax.
- **Follow the skill structure** → [`ARCHITECTURE.md`](docs/ARCHITECTURE.md), use `/jai-context:04-skill-generate` to scaffold a new one.
- **One concern per commit** — Conventional Commits format, imperative mood.

## 📚 Reference

[`ARCHITECTURE.md`](docs/ARCHITECTURE.md) · [`CREATE_PLUGIN.md`](docs/CREATE_PLUGIN.md) · [`GLOSSARY.md`](docs/GLOSSARY.md) · [`COMMANDS.md`](COMMANDS.md) — quick reference for every `jai-*` skill.

---

■ [Back to framework](./README.md)
