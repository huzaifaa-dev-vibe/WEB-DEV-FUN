# AI_AGENT_GUIDE

> Read this file FIRST. It tells you (the AI coding agent) how to use this repository without hallucinating, without producing generic AI-looking output, and without skipping the steps that matter.

This file is the contract between this repository and any LLM-based coding agent (Claude, GPT, Cursor, Cline, Aider, Devin, Copilot, Continue, etc.) that reads it.

---

## Purpose

You are an AI coding agent. You have been given this repository as a reference manual. Your job is to plan, build, review, debug, and ship web applications. This file tells you:

1. How to navigate this repository deterministically.
2. How to make technology decisions instead of guessing.
3. How to plan projects without skipping steps.
4. How to write code that doesn't look AI-generated.
5. How to verify your output before claiming success.
6. How to know when to stop and ask the human.

---

## Prerequisites

- You can read markdown.
- You can call tools (read files, write files, run shell commands, web search).
- You have a working directory under `/home/z/my-project/` (or equivalent).
- You understand that hallucinated APIs, made-up package names, and invented config keys are **critical defects**, not minor bugs.

---

## Learning Outcome

After internalizing this file, you can:

- Find any answer in this repository in ≤3 hops.
- Produce project plans that a senior engineer would approve.
- Write code that passes the "does this look AI-generated?" test (see [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/)).
- Self-verify your output before reporting "done".
- Decide autonomously when to ask the human vs. proceed.

---

## Dependencies

- This repository (you're reading it).
- A code editor or filesystem access.
- Optionally: a browser, a shell, a package manager.

---

## Related Files

- [INDEX.md](INDEX.md) — table of contents
- [ROADMAP.md](ROADMAP.md) — learning/dependency order
- [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) — tool/library selection
- [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) — required reading before any UI work
- [PROMPTS.md](PROMPTS.md) — reusable prompt templates
- [COMMON_MISTAKES.md](COMMON_MISTAKES.md) — known traps
- [Checklists/](Checklists/) — pre-flight, pre-launch

---

## How to Navigate This Repository (Deterministic Routing)

Do NOT free-associate. Do NOT guess where things are. Follow this routing table.

| You need to... | Go to |
|---|---|
| Pick a tech stack | [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) |
| Pick a rendering strategy (SSR/SSG/CSR/ISR) | [Templates/_next-app/](Templates/) |
| Pick a color palette | [Color-Palettes/](Color-Palettes/) |
| Pick a font pairing | [Typography/](Typography/) |
| Decide between REST and GraphQL | [APIs/](APIs/README.md#rest-vs-graphql) |
| Decide between JWT, sessions, OAuth, Passkeys | [Authentication/](Authentication/README.md#decision-tree) |
| Decide between Postgres, Mongo, Redis | [Databases/](Databases/README.md#decision-tree) |
| Decide between Prisma and Drizzle | [ORM/](ORM/README.md#prisma-vs-drizzle) |
| Decide between Vercel, Netlify, Cloudflare, AWS | [Deployment/](DEPLOYMENT.md#decision-tree) |
| Build a specific type of site | [Website-Blueprints/](Website-Blueprints/) |
| Find a project spec | [Projects/](Projects/) |
| Find a code skeleton | [Templates/](Templates/) |
| Make UI not look AI-generated | [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/) |
| Run a pre-flight check | [Checklists/](Checklists/pre-flight.md) |
| Run a pre-launch check | [Checklists/](Checklists/pre-launch.md) |
| Diagnose an error | [ERRORS.md](ERRORS.md) |
| Debug systematically | [DEBUGGING.md](DEBUGGING.md) |
| Write a prompt for another agent | [PROMPTS.md](PROMPTS.md) |

---

## How to Make Technology Decisions

**NEVER** pick a library because "it's popular" or "I've seen it before". ALWAYS follow this procedure:

1. **State the constraint** — What is the actual hard requirement? (Latency? Cost? Team familiarity? Type safety? Bundle size?)
2. **List candidates** — Use [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) to enumerate 2–5 options.
3. **Check the decision table** — Most folders have a "Decision Tree" section. Use it.
4. **Verify existence** — Run `npm view <package>` or `gh repo view <owner>/<repo>` to confirm the package/repo exists and is maintained. If you cannot verify, do NOT pick it.
5. **Verify version** — Check the latest stable version. Pin it. Do not use `^` for new deps in production.
6. **Document the choice** — In your plan, write: "Chose X over Y because <constraint>. Verified at <version> on <date>."

If you cannot complete step 4, STOP and tell the human. Do not invent package names.

---

## How to Plan Projects (The Mandatory Procedure)

Before writing ANY code for a new project, produce a plan document with these sections. Save it as `PLAN.md` in the project root.

```markdown
# PLAN — <project name>

## 1. Problem statement
What user problem does this solve? One paragraph. No tech.

## 2. Users & personas
Who uses this? What do they want? What stops them today?

## 3. Scope (in / out)
- IN: <explicit list>
- OUT: <explicit list>

## 4. Functional requirements
- As a <user>, I can <action>, so that <benefit>.

## 5. Non-functional requirements
- Performance: <LCP target, INP target, p99 latency>
- Scale: <users, RPS, data volume>
- Security: <auth model, threat model summary>
- Accessibility: <WCAG level>
- Browser support: <matrix>

## 6. Tech stack (with verification)
| Layer | Choice | Verified | Why |
|---|---|---|---|
| Frontend | Next.js 15 | ✅ npm view | App Router, RSC |
| ... | ... | ... | ... |

## 7. Architecture
ASCII diagram + 1 paragraph explaining data flow.

## 8. Data model
Tables/collections with fields, types, indexes, relationships.

## 9. Folder structure
Tree with one-line purpose per top-level folder.

## 10. Rendering strategy
Per-route table: SSR / SSG / ISR / CSR / streaming.

## 11. Auth model
Flow diagram + token storage + refresh strategy.

## 12. Testing strategy
Unit / integration / E2E split. Coverage targets.

## 13. Deployment
Provider, environment variables, secrets, CI/CD pipeline.

## 14. Observability
Logs, metrics, traces, alerts, dashboards.

## 15. Risks
Top 5 risks + mitigation.

## 16. Milestones
M1 → M2 → ... with acceptance criteria.

## 17. Open questions
What you need the human to decide.
```

**Only after this plan is written and (preferably) reviewed, write code.**

---

## How to Write Code That Doesn't Look AI-Generated

This is non-negotiable. Before producing any UI, READ [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/). Summary of the rules:

1. **No "gradient hero with centered headline + 2 CTAs + 3 feature cards"** unless the user explicitly asked for that. Pick a real layout from [Website-Blueprints/](Website-Blueprints/).
2. **No emoji icons.** Use real SVG icons from [Icons/](Icons/).
3. **No `Lorem ipsum`.** Write real copy, or use the human's copy, or ask for it.
4. **No `text-3xl font-bold` everywhere.** Build a real type scale from [Typography/](Typography/).
5. **No identical card grids.** Vary rhythm, alignment, and density.
6. **No purple-to-pink gradients by default.** Pick a palette with intent from [Color-Palettes/](Color-Palettes/).
7. **No `rounded-2xl` on everything.** Mix radii intentionally.
8. **No fake testimonials with stock photo avatars and 5 stars.**
9. **Real spacing rhythm.** Use a scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96).
10. **Real motion.** Animations should have purpose. See [Animations/](Animations/).

---

## How to Verify Your Output (Self-Check Before Reporting Done)

Before telling the human "I'm done", run through this checklist:

### Code verification
- [ ] Does the code run? (`npm install && npm run build` exits 0)
- [ ] Does it pass lint? (`npm run lint` exits 0)
- [ ] Does it pass types? (`tsc --noEmit` exits 0)
- [ ] Did I run any tests I wrote? (`npm test`)
- [ ] Did I verify every imported package exists at the version I specified?
- [ ] Did I verify every external URL/link I referenced is reachable?

### UI verification
- [ ] Did I check it in a browser (or screenshot)? Don't claim visual things work without looking.
- [ ] Mobile viewport (375px) — no horizontal scroll, no overflow.
- [ ] Desktop viewport (1440px) — no awkward whitespace, no broken layout.
- [ ] Dark mode (if applicable) — text is readable.
- [ ] Keyboard nav — Tab order is sensible, focus visible.
- [ ] Lighthouse run — LCP < 2.5s, CLS < 0.1, INP < 200ms.

### Correctness verification
- [ ] Did I actually implement every requirement in the spec?
- [ ] Did I handle the error cases (empty state, loading state, error state)?
- [ ] Did I handle the empty-string / null / undefined cases?
- [ ] Did I write the security headers / input validation / auth checks?
- [ ] Did I update the README / docs to reflect what I built?

### Anti-AI verification
- [ ] Run through [ANTI-AI-DESIGN/checklist.md](ANTI-AI-DESIGN/checklist.md). Fix any failure.

### "Did I hallucinate?" verification
- [ ] Every API/function name I called — does it exist? (check docs or `tsc`)
- [ ] Every config key I set — is it a real key? (check the package's docs)
- [ ] Every CLI flag I used — does it exist? (run `--help`)
- [ ] Every version number I pinned — does it exist? (`npm view`)
- [ ] Every claim about "this library does X" — did I verify, or am I guessing?

If ANY of the above fails, do not report done. Fix it or report the blocker.

---

## How to Avoid Hallucinations

| Hallucination type | Cause | Fix |
|---|---|---|
| Invented package name | Pattern-matched from similar names | `npm view <pkg>` before importing |
| Invented API method | Confused with another library | Read the actual docs / source |
| Invented CLI flag | Guessed from convention | `<cmd> --help` |
| Invented config key | Copied from a different version | Read the package's current docs |
| Invented file path | Assumed convention | `ls` the directory |
| Wrong type signature | Guessed from name | `tsc --noEmit` |
| Wrong HTTP status | Guessed | Check [REST/](REST/status-codes.md) |
| Wrong CSS property | Confused with similar | Check MDN |
| Invented company / brand | Pattern completion | Don't invent. Use placeholder. |

**Core rule:** if you cannot verify a claim within 30 seconds, either verify it with a tool or hedge it explicitly: "I believe X, but please verify."

---

## How to Cooperate with Humans

### Ask for clarification when:
- The spec has multiple valid interpretations.
- The constraint is missing (budget, timeline, audience, browser support).
- You're about to make an irreversible decision (delete data, ship to prod, spend money).
- You've hit 2+ consecutive failures on the same task (see Rule 12 in the system prompt).

### Don't ask when:
- The answer is in this repo. Look it up.
- The answer is on the package's docs. Look it up.
- The decision is reversible and low-stakes. Make the call, document it.
- You're just nervous. Re-read the spec.

### Communication style with humans:
- Lead with status (done / blocked / in progress / needs decision).
- Then the one thing they need to know.
- Then context, if they want it.
- Never bury a blocker in paragraph 4.

---

## How to Read the Rest of This Repository

Every folder README follows this template:

```
Purpose → Prerequisites → Learning Outcome → Dependencies →
Related Files → AI Instructions → Human Notes → References →
Further Reading → Exercises → Projects
```

The **AI Instructions** section is written for you. The **Human Notes** section is opinionated context. The **References** section is authoritative external links — use them when this file isn't enough.

---

## How to Use PROMPTS.md

[PROMPTS.md](PROMPTS.md) contains reusable prompt templates for common tasks:

- Generate a project spec
- Generate a component
- Generate a test
- Review code
- Refactor code
- Write a migration
- Debug an error
- Write a README

Copy the relevant template, fill in the placeholders, run it.

---

## Operating Loop

When you receive a task, follow this loop:

```
1. Parse intent → what does the human actually want?
2. Locate relevant files in this repo (use the routing table above).
3. Read those files completely. Do not skim.
4. Write PLAN.md (if project) or note the steps (if task).
5. Execute step by step. Verify after each step.
6. When blocked: stop, report, ask. Do not flail.
7. Self-verify using the checklist above.
8. Report done with: what you did, how to run it, what's next, what's risky.
```

---

## Forbidden Behaviors

- ❌ Producing UI without reading [ANTI-AI-DESIGN/](ANTI-AI-DESIGN/).
- ❌ Picking libraries without verifying they exist.
- ❌ Skipping the plan and going straight to code on anything > 1 file.
- ❌ Reporting "done" without running the self-check.
- ❌ Inventing APIs, config keys, or CLI flags.
- ❌ Silently retrying failed tool calls > 2 times without telling the human.
- ❌ Writing fake copy and calling it done.
- ❌ Shipping without security headers / input validation.
- ❌ Skipping accessibility because "it's a prototype".
- ❌ Long AI-looking paragraphs (3 paragraphs of generic intro before the answer).

---

## Required Behaviors

- ✅ Read the relevant folder before writing code in that domain.
- ✅ Verify package existence and version before importing.
- ✅ Write a PLAN.md for projects of any size.
- ✅ Run the self-check before reporting done.
- ✅ Tell the human when you're guessing.
- ✅ Tell the human when you're blocked.
- ✅ Keep copy real. Keep UI human.
- ✅ Run checklists from [Checklists/](Checklists/) before shipping.
- ✅ Leave the codebase better than you found it.

---

## Final Note

You are not a search engine. You are not a tutorial generator. You are an engineer with a reference library (this repo). Use the library. Verify your work. Ship things that don't suck.

**Next:** [INDEX.md](INDEX.md) · [START-HERE.md](START-HERE.md) · [PROMPTS.md](PROMPTS.md)
