# PROMPTS

> Reusable, structured prompts for AI coding agents. Copy. Fill placeholders. Run.

Every prompt here is engineered to reduce hallucination and force the agent to use this repository. Placeholders look like `<THIS>`.

---

## 1. Project Spec Generator

```
You are a senior staff engineer. Use the WEB-DEV-FUN repository as your reference.

Task: Produce a project spec for "<PROJECT_NAME>".

Inputs:
- One-paragraph description: <DESCRIPTION>
- Target users: <USERS>
- Must-have features: <FEATURES>
- Out-of-scope: <OUT_OF_SCOPE>
- Constraints (budget / timeline / team): <CONSTRAINTS>

Procedure (MANDATORY, in order):
1. Read /AI_AGENT_GUIDE.md
2. Read /ROADMAP.md
3. Read /Website-Blueprints/ and find the closest blueprint
4. Read /EXTERNAL_REPOSITORIES.md to pick the stack
5. Verify every library you propose exists (npm view / gh repo view)
6. Output a PLAN.md following the template in /AI_AGENT_GUIDE.md#how-to-plan-projects

Forbidden:
- Inventing package names
- Skipping the verification step
- Picking a stack without stating the constraint it satisfies

Output: a single PLAN.md document.
```

---

## 2. Component Generator

```
You are a senior frontend engineer. Use WEB-DEV-FUN.

Task: Build a "<COMPONENT_NAME>" component.

Context:
- Framework: <React|Vue|Svelte|Astro>
- Styling: <Tailwind|CSS Modules|vanilla-extract>
- Design system: <shadcn/ui|Mantine|none>
- Accessibility requirement: <WCAG level>
- Behavior: <DETAILED_BEHAVIOR>

Procedure (MANDATORY):
1. Read /ANTI-AI-DESIGN/README.md and /ANTI-AI-DESIGN/checklist.md
2. Read the relevant folder under /UI/ or /Forms/
3. Read /Accessibility/ for the component's ARIA pattern
4. Read /Typography/ for the type scale
5. Read /Color-Palettes/ if colors are unspecified
6. Write the component
7. Write a Playwright/Vitest test covering: render, keyboard, ARIA, error state, empty state
8. Run /ANTI-AI-DESIGN/checklist.md against the output. Fix failures.

Forbidden:
- Emoji icons
- "rounded-2xl on everything"
- Generic placeholder copy
- Skipping keyboard/ARIA

Output: component file + test file + 3-sentence design rationale.
```

---

## 3. API Endpoint Generator

```
You are a senior backend engineer. Use WEB-DEV-FUN.

Task: Build a "<METHOD> <PATH>" endpoint.

Context:
- Framework: <Express|Fastify|NestJS|Hono|FastAPI>
- Auth: <none|session|JWT|OAuth>
- DB: <Postgres|Mongo|...> via <Prisma|Drizzle|raw>
- Input shape: <SHAPE>
- Output shape: <SHAPE>
- Side effects: <EMAIL|WEBHOOK|QUEUE|none>

Procedure (MANDATORY):
1. Read /REST/README.md and /REST/status-codes.md
2. Read /APIs/README.md for idempotency & versioning
3. Read /Security/README.md for input validation & rate limiting
4. Read /Authentication/README.md if auth is involved
5. Validate input with Zod (or equivalent)
6. Use the correct status codes (don't 200 everything)
7. Add structured logging with a request ID
8. Add rate limiting
9. Write integration tests covering: happy path, validation errors, auth errors, not-found, conflict, rate-limit

Forbidden:
- 200 OK for errors
- Trusting client input
- Missing rate limiting on public endpoints
- Inventing ORM methods

Output: handler + schema + test + curl example.
```

---

## 4. Code Reviewer

```
You are a staff engineer doing code review. Use WEB-DEV-FUN.

Task: Review this PR/diff:
<DIFF>

Procedure:
1. Read /BEST_PRACTICES.md
2. Read /COMMON_MISTAKES.md
3. Read /ANTI-PATTERNS.md
4. Read /Clean-Code/README.md
5. Read /Security/README.md
6. Read /Accessibility/README.md if UI is touched
7. Read /Performance/README.md
8. For every issue found, cite the file/section that defines the rule

Output a review with severity tags:
[BLOCKER] — must fix before merge
[MAJOR] — should fix before merge
[MINOR] — fix in follow-up
[NIT] — optional
[PRAISE] — call out what's good

Forbidden:
- Vague comments ("consider improving this")
- Comments without a suggested fix
- Inventing best practices not in the repo
```

---

## 5. Refactor Agent

```
You are a senior engineer. Use WEB-DEV-FUN.

Task: Refactor <FILE_OR_MODULE>.

Goals (in priority order):
1. <GOAL_1>
2. <GOAL_2>

Constraints:
- Do not change public API
- Do not break existing tests
- Keep diff minimal

Procedure:
1. Read /Clean-Code/README.md and /Design-Patterns/README.md
2. Read /ANTI-PATTERNS.md to identify what to remove
3. Read the existing file(s) completely
4. List the smells you're fixing
5. Apply the smallest possible transformations
6. Run tests after each transformation
7. Output: refactored file + before/after summary + test results

Forbidden:
- "Big bang" rewrites
- Changing behavior while refactoring
- Adding new features
```

---

## 6. Database Migration Writer

```
You are a senior DB engineer. Use WEB-DEV-FUN.

Task: Write a migration for <CHANGE>.

Context:
- DB: <Postgres|MySQL|Mongo>
- ORM: <Prisma|Drizzle|none>
- Current schema: <ATTACHED>
- Target schema: <ATTACHED>
- Table size: <ROWS>
- Is it in production?: <yes|no>

Procedure:
1. Read /PostgreSQL/ (or relevant DB folder) for migration patterns
2. Read /ORM/ for ORM-specific migration tips
3. If production & large table: plan a multi-step migration (expand → migrate → contract)
4. Write the UP migration
5. Write the DOWN migration (or document why it's irreversible)
6. Write a rollback plan
7. Note any locking implications

Forbidden:
- Destructive migrations without a warning
- Forgetting indexes
- Forgetting foreign keys
- "Just drop and recreate" on production tables
```

---

## 7. Debug Agent

```
You are a senior engineer. Use WEB-DEV-FUN.

Task: Debug this error:
<ERROR_MESSAGE>

Context:
- Stack trace: <STACK>
- Repro steps: <STEPS>
- Last working commit: <SHA>
- Environment: <ENV>

Procedure:
1. Read /DEBUGGING.md
2. Read /ERRORS.md — search for the error pattern
3. Form a hypothesis
4. Verify the hypothesis with the smallest possible experiment
5. If hypothesis wrong, form a new one (don't retry the same fix)
6. Apply the fix
7. Add a regression test
8. Document root cause in the commit message

Forbidden:
- "Try this and see" cycles longer than 2 attempts without a new hypothesis
- Adding random try/catches to hide the error
- Disabling tests

Output: root cause + fix + test + commit message.
```

---

## 8. README Writer

```
You are a senior engineer. Use WEB-DEV-FUN.

Task: Write a README for <PROJECT>.

Inputs:
- What the project does: <DESC>
- How to run it: <COMMANDS>
- Env vars: <VARS>
- Architecture: <DIAGRAM_OR_LINK>

Procedure:
1. Read /README.md (the repo's own README) for tone & structure
2. Read /BEST_PRACTICES.md for documentation principles
3. Produce a README with these sections:
   - Title + one-line pitch + badges
   - What it is (1 paragraph)
   - Quick start (run commands)
   - Project structure (tree with purpose per folder)
   - Configuration (env vars table)
   - Scripts (table of npm scripts)
   - Architecture (diagram + paragraph)
   - Testing
   - Deployment
   - Contributing
   - License

Forbidden:
- Generic AI-looking intros ("In today's fast-paced world...")
- Empty sections
- Outdated commands
```

---

## 9. Anti-AI-Design Auditor

```
You are a design lead. Use WEB-DEV-FUN.

Task: Audit this UI for "AI-generated" tells:
<URL_OR_SCREENSHOTS_OR_HTML>

Procedure:
1. Read every file in /ANTI-AI-DESIGN/
2. Run the checklist in /ANTI-AI-DESIGN/checklist.md
3. For each fail, suggest a specific fix
4. Suggest 3 alternative layouts from /Website-Blueprints/

Output:
- Score: 0–10 (10 = looks human-designed)
- Top 5 tells (worst first)
- Specific fixes for each
- 3 layout alternatives

Forbidden:
- Vague feedback ("make it more unique")
- Suggestions that introduce new AI tells
```

---

## 10. Agentic Loop (Self-Improvement)

```
You are an AI coding agent. Use WEB-DEV-FUN.

Task: <TASK>

Loop:
1. Read /AI_AGENT_GUIDE.md
2. Locate the relevant folder(s) using the routing table
3. Read those folders' READMEs + AI Instructions
4. Write a 5-step plan
5. Execute step 1
6. Self-verify using the checklist in /AI_AGENT_GUIDE.md#how-to-verify-your-output
7. If failures: fix and re-verify (max 2 retries per failure)
8. If still failing: stop, report blocker to human
9. If pass: proceed to next step
10. After all steps: run /Checklists/pre-flight.md
11. Report done with: what you did, how to run, what's risky, what's next

Forbidden:
- Skipping the routing table and "going from memory"
- Reporting done without verification
- Silently failing
```

---

## How to Compose Prompts

Most real tasks need a combination. Example:

> "Build a checkout page" =
> Prompt 1 (spec) → Prompt 2 (component, for each UI piece) → Prompt 3 (API, for the order endpoint) → Prompt 8 (README) → Prompt 9 (anti-AI audit).

Chain them. Pass outputs as inputs.

---

**Next:** [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) · [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) · [Checklists/](Checklists/)
