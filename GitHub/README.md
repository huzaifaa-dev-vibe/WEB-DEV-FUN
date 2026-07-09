# GitHub

> Code hosting, PRs, issues, Actions, Projects, security features.

---

## Purpose

Use GitHub effectively: PRs, Actions, Projects, security, discussions.

## Prerequisites

- [Git/](../Git/).

## Learning Outcome

You can configure a GitHub repo for team productivity and security.

## Dependencies

- GitHub account.

## Related Files

- [Git/](../Git/) · [CI-CD/](../CI-CD/) · [CONTRIBUTING.md](../CONTRIBUTING.md)

## AI Instructions

When using GitHub:
1. **Branch protection** on main: require PR, require review, require status checks.
2. **GitHub Actions** for CI/CD.
3. **Dependabot** for dep updates.
4. **CodeQL** for security scans.
5. **Discussions** for Q&A.
6. **Projects** for project management.
7. **Releases** for versioned releases.

## Human Notes

### Repo settings
- **Branch protection**:
  - Require PR before merge.
  - Require 1+ reviews.
  - Require status checks (CI).
  - Require branches up-to-date.
  - No force push.
  - No force push to main.
- **Secrets** in repo/org secrets.
- **Environments** for staging/prod separation.
- **Required reviewers** for prod env.

### Pull requests
- Title + description.
- Link to issue.
- Screenshots for UI changes.
- Test plan.
- Reviewers.
- Labels (bug, feature, etc.).
- Auto-assign.

### GitHub Actions
- Workflows in `.github/workflows/`.
- Pin actions by SHA (security).
- Use `actions/cache` for speed.
- Use `actions/upload-artifact` to share files.

### Dependabot
Auto-opens PRs for dep updates. Configure:
```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: /
    schedule:
      interval: weekly
  - package-ecosystem: github-actions
    directory: /
    schedule:
      interval: weekly
  - package-ecosystem: docker
    directory: /
    schedule:
      interval: weekly
```

### CodeQL
GitHub's static analysis for security. Free for public repos.

### GitHub Container Registry (ghcr.io)
Host Docker images alongside code.

### GitHub Pages
Free static hosting from a repo.

### GitHub Projects
- Kanban boards.
- Issue tracking.
- Roadmaps.
- Linked to PRs.

### GitHub Discussions
- Q&A.
- Announcements.
- Long-form discussions.

### GitHub Releases
- Tag-based.
- Auto-generated release notes.
- Binary assets.

### GitHub CLI (gh)
```bash
gh pr create --fill
gh pr checkout 123
gh pr merge --squash
gh repo clone owner/repo
gh issue create
gh release create v1.0.0 ./dist/*
gh workflow run
gh run watch
```

### Security features
- **Dependabot** alerts + PRs.
- **CodeQL** analysis.
- **Secret scanning** (push protection).
- **Security advisories**.
- **Security policy** (`SECURITY.md`).
- **CODEOWNERS** for auto-assign.

### CODEOWNERS
```
* @maintainers
/src/auth/ @auth-team
/src/payments/ @payments-team
```

### Issue templates
`.github/ISSUE_TEMPLATE/`:
- bug.yml
- feature.yml
- config.yml

### PR template
`.github/PULL_REQUEST_TEMPLATE.md`.

## Common Mistakes

- ❌ No branch protection.
- ❌ Actions pinned to `@v1` (use SHA).
- ❌ Secrets in code.
- ❌ No Dependabot.
- ❌ Big PRs without description.
- ❌ Merging without review.
- ❌ No CI.
- ❌ Force-pushing to main.

## Tools

- GitHub docs: https://docs.github.com/
- GitHub CLI: https://cli.github.com/
- GitHub Actions marketplace: https://github.com/marketplace

## References

- GitHub docs: https://docs.github.com/
- GitHub security: https://docs.github.com/code-security

## Exercises

1. Set up branch protection + required reviews.
2. Add Dependabot + CodeQL.
3. Set up CI with GitHub Actions.

## Projects

- Open-source a project with full GitHub setup (templates, Actions, security).

---

**Previous:** [Git/](../Git/) · **Next:** [Linux/](../Linux/) · **Related:** [CI-CD/](../CI-CD/)
