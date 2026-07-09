# Git

> Version control. The most important tool in software.

---

## Purpose

Master Git: branches, merges, rebases, hooks, workflows.

## Prerequisites

- Command line basics.

## Learning Outcome

You can use Git effectively solo and in teams.

## Dependencies

- Git installed.

## Related Files

- [GitHub/](../GitHub/) · [CI-CD/](../CI-CD/) · [CHEATSHEET.md#git](../CHEATSHEET.md#git)

## AI Instructions

When using Git:
1. **Conventional Commits** (`feat:`, `fix:`, etc.).
2. **Small commits**, one concern each.
3. **Pull requests** for merging into main.
4. **Rebase** your branch before merge.
5. **Never force push** to shared branches.
6. **`.gitignore`** for node_modules, .env, build artifacts.
7. **pre-commit hooks** for lint/format.

## Human Notes

### Config
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global core.pager delta
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"
```

### Daily workflow
```bash
git checkout -b feat/my-feature
# ... code ...
git add .
git commit -m "feat: add login form"
git push -u origin feat/my-feature
# open PR
# review
# merge
git checkout main
git pull
git branch -d feat/my-feature
```

### Branching strategies
- **Trunk-based** (recommended) — short-lived branches, frequent merges to main. Feature flags for unfinished work.
- **GitHub Flow** — feature branch → PR → merge to main → deploy.
- **Git Flow** — develop branch + release branches. Older, more complex.
- **GitLab Flow** — environment branches.

### Rebasing
Replay your commits on top of another branch.
```bash
git checkout feat/my-feature
git rebase main
# resolve conflicts if any
git push --force-with-lease
```

Rebase keeps history linear. Use it.

### Squashing
Combine commits:
```bash
git rebase -i HEAD~3
# pick first, squash others
```

Or squash-merge on GitHub.

### Stash
```bash
git stash
git stash pop
git stash list
git stash drop
```

### Reflog (lifesaver)
```bash
git reflog
git reset --hard HEAD@{5}
```

### Bisect
Find the commit that broke something:
```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
# test, then mark
git bisect good  # or bad
git bisect reset
```

### Hooks
- Pre-commit: lint, format, secrets check.
- Pre-push: tests.
- Commit-msg: enforce Conventional Commits.

Use `pre-commit` framework: https://pre-commit.com/

### .gitignore
```
node_modules/
.next/
dist/
.env
.env.local
*.log
.DS_Store
.idea/
.vscode/
coverage/
```

Use https://gitignore.io or GitHub's templates.

### Tags
```bash
git tag v1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin v1.0.0
```

### Submodules
Git repos inside git repos. Avoid if possible — use monorepo or package manager.

### LFS (Large File Storage)
For binary files (videos, large images). Avoid committing large binaries to git.

### Monorepo tools
- Turborepo.
- Nx.
- pnpm workspaces.

## Common Mistakes

- ❌ `git push --force` to shared branches.
- ❌ Committing secrets.
- ❌ Committing `node_modules` / build artifacts.
- ❌ Huge PRs (1000+ files).
- ❌ Long-lived feature branches.
- ❌ "WIP" commits in main.
- ❌ No commit messages.
- ❌ `git merge` everywhere (use rebase for clean history).
- ❌ Ignoring `.gitignore`.

## Tools

- Git docs: https://git-scm.com/docs
- Lazygit (TUI): https://github.com/jesseduffield/lazygit
- Tig (TUI): https://github.com/jonas/tig
- GitKraken (GUI): https://www.gitkraken.com/
- Sublime Merge: https://www.sublimemerge.com/
- GitHub Desktop: https://desktop.github.com/
- pre-commit: https://pre-commit.com/
- git-secrets: https://github.com/awslabs/git-secrets

## References

- Pro Git (free book): https://git-scm.com/book/
- Atlassian Git tutorials: https://www.atlassian.com/git/tutorials
- Oh Shit, Git!?!: https://ohshitgit.com/

## Further Reading

- *Pro Git* — Scott Chacon (free)

## Exercises

1. Use `git bisect` to find a bug.
2. Recover a deleted branch with `git reflog`.
3. Set up pre-commit hooks.

## Projects

- Set up a Git workflow for a team (CONTRIBUTING.md, branch protection, hooks).

---

**Previous:** [CI-CD/](../CI-CD/) · **Next:** [GitHub/](../GitHub/) · **Related:** [CONTRIBUTING.md](../CONTRIBUTING.md)
