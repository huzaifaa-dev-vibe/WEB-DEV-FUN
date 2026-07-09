# CONTRIBUTING

> How to contribute to WEB-DEV-FUN. Read before your first PR.

---

## Purpose

Make contributing easy, consistent, and useful. Every contribution should leave the repo better.

## Prerequisites

- A GitHub account.
- Markdown skills.
- Something useful to add.

## Learning Outcome

You can submit a PR that gets merged.

## Related Files

- [README.md](README.md)
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) (add if missing)
- [STYLE.md](STYLE.md) (this file serves as partial style guide)
- [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) — for AI agents contributing

## Ways to Contribute

- **Fix typos / broken links.** Always welcome.
- **Improve existing content.** Make it clearer, more accurate, more complete.
- **Add new sections.** See "Adding New Sections" below.
- **Add examples / projects / templates.**
- **Report issues.** Use GitHub Issues.
- **Suggest improvements.** Open a discussion first for big changes.

## File Template

Every new markdown file MUST follow the standard template:

```markdown
# <Topic Name>

> One-sentence pitch.

## Purpose
Why this file exists.

## Prerequisites
What you should already know.

## Learning Outcome
What you'll be able to do.

## Dependencies
Tools/libs/sibling files this depends on.

## Related Files
Links to closely-related files.

## AI Instructions
What an AI agent should do with this file.

## Human Notes
Context, opinions, gotchas.

## References
Authoritative external links.

## Further Reading
Books, courses, articles.

## Exercises
Hands-on tasks.

## Projects
End-to-end projects.
```

## Style Guide

### Markdown
- Use ATX-style headings (`#`, not `===` underline).
- Use fenced code blocks with language tags.
- Use tables for comparisons.
- Use lists for steps.
- Maximum line length: 120 chars (where reasonable).
- Trailing newline at end of file.

### Voice
- Direct. No fluff.
- Active voice.
- "You" not "we".
- Short sentences.
- Concrete examples.

### Links
- Relative links within the repo.
- HTTPS for external.
- Anchor text describes the target. No "click here".
- Verify links work before submitting.

### Code
- Always specify language in fences.
- Test the code. If it doesn't run, don't include it.
- Use modern syntax (ES2022+, TS, etc.).
- Comment the WHY, not the WHAT.

### Numbers
- Use digits for numbers (12, not twelve), except for small counts.
- Use K / M / B for large (4K, 1.2M).

## Adding New Sections

1. **Discuss first.** Open a GitHub Discussion or Issue. Get alignment.
2. **Pick the right folder.** Check [INDEX.md](INDEX.md).
3. **Create the README.md** following the file template.
4. **Add supplementary files** (examples, best-practices, cheat-sheet, etc.) as needed.
5. **Update INDEX.md** with the new entry.
6. **Update relevant nav links** in adjacent files.
7. **Test every link.**
8. **Open a PR** with a clear description.

## Adding a New Topic Folder

A topic folder should contain:
- `README.md` — main file, follows template
- `best-practices.md` — dos and don'ts
- `cheat-sheet.md` — quick reference
- `examples/` — code samples
- `resources.md` — links
- `exercises.md` — practice tasks
- `common-mistakes.md` — pitfalls

Not every folder needs every file. Don't pad.

## Commit Messages

Conventional Commits:
- `feat: add Vue 3 composition API guide`
- `fix: broken link in CSS README`
- `docs: clarify Web Vitals targets`
- `refactor: reorganize AI folder`
- `chore: bump dependencies`

## Pull Request Process

1. **Branch from `main`.** Name it `feat/...`, `fix/...`, `docs/...`.
2. **One concern per PR.**
3. **Small PRs.** < 400 lines diff ideal.
4. **PR description** must include:
   - What changed
   - Why
   - How to verify
   - Checklist: [ ] tests pass, [ ] links work, [ ] file template followed
5. **Self-review** before requesting review.
6. **Respond to every comment** (even with "agree, will follow up").
7. **Rebase** on main before merge.
8. **Squash merge** unless commits tell a story.

## Review Criteria

Reviewers will check:
- Accuracy (technical correctness).
- Completeness (covers the topic usefully).
- Clarity (understandable by target audience).
- Consistency (follows repo style).
- Links work.
- File template followed.
- No plagiarism (cite sources).
- No AI-generated slop (you can use AI tools, but the output must be reviewed and human-quality).

## Code of Conduct

Be kind. Be constructive. Be inclusive. No harassment, no personal attacks, no spam. Disagree on the tech, not the person.

## Attribution

- Cite sources for non-original content.
- Respect licenses (most tech docs are CC-BY or similar; quote briefly with link).
- Don't copy-paste large blocks from other sources.

## AI Agent Contributions

AI agents are welcome to contribute, but:
- The PR description MUST note that the PR was AI-generated.
- A human MUST review and approve before merge.
- The AI MUST follow [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md).
- No hallucinated packages, APIs, or links.
- Verify everything before submitting.

## License

By contributing, you agree your contributions are licensed under the MIT license. See [LICENSE](LICENSE).

## Recognition

All contributors are recognized in the README. (Add a Contributors section if it doesn't exist.)

---

Thanks for making WEB-DEV-FUN better.

---

**Next:** [README.md](README.md) · [INDEX.md](INDEX.md) · [CHANGELOG.md](CHANGELOG.md)
