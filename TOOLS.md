# TOOLS

> The recommended toolkit. The 80% case. Deviate when you have a real reason.

This file is opinionated. It's the toolkit a senior engineer would set up on a new laptop today. → [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) for libraries (not standalone tools).

---

## Editor & Editor Ecosystem

### Primary: VS Code
- **Download:** https://code.visualstudio.com/
- **Why:** Industry default. Huge extension ecosystem. Free. Works everywhere.

**Essential extensions:**
- ESLint
- Prettier
- Tailwind CSS IntelliSense
- GitLens
- Error Lens
- Docker
- Remote - Containers / SSH / WSL
- GitHub Pull Requests
- Live Share (pairing)
- Path Intellisense
- Auto Rename Tag
- Console Ninja
- Pretty TypeScript Errors

### Alternative: Cursor
- **Download:** https://cursor.sh/
- **Why:** VS Code fork with AI baked in. Best AI-assisted editing today.

### Alternative: Zed
- **Download:** https://zed.dev/
- **Why:** Fast (Rust). Minimal. Good for big files.

### Alternative: Vim / Neovim
- **Why:** Once learned, fastest editing. Highly customizable.
- **Distribution:** LazyVim, AstroNvim, NvChad.

### Alternative: JetBrains (WebStorm / PyCharm / RustRover / IntelliJ)
- **Why:** Best refactoring, DB tools, integrated everything. Paid.

### Browser DevTools
- Chrome DevTools (built-in)
- React DevTools (extension)
- Vue DevTools (extension)
- Redux DevTools (extension)
- Svelte DevTools (extension)
- Angular DevTools (extension)
- Lighthouse (built-in)
- axe DevTools (extension, a11y)
- Web Developer (extension)
- Wappalyzer (extension, tech detection)
- Vue Telescope (extension)

### Browser (for development)
- Chrome / Chromium — primary
- Firefox — secondary (different engine, different bugs)
- Safari — for cross-browser testing (especially mobile)
- Edge — for testing on Windows
- Brave — for privacy testing

---

## Terminal & Shell

### Terminal emulators
- **iTerm2** (macOS) — https://iterm2.com/
- **Warp** (macOS/Linux) — https://www.warp.dev/ (AI-assisted)
- **WezTerm** (cross-platform) — https://wezfurlong.org/wezterm/
- **Alacritty** (cross-platform, fast) — https://alacritty.org/
- **Kitty** (cross-platform) — https://sw.kovidgoyal.net/kitty/
- **Windows Terminal** (Windows) — https://aka.ms/terminal

### Shells
- **Zsh** (default on macOS) — with Oh My Zsh / Prezto / Zinit
- **Fish** (friendlier, less scriptable) — https://fishshell.com/
- **Nushell** (structured shell) — https://www.nushell.sh/

### Prompt
- **Starship** — https://starship.rs/ (cross-shell, language-aware)
- **Powerlevel10k** — Zsh-only, very fast

### Multiplexer
- **tmux** — https://github.com/tmux/tmux
- **Zellij** — https://zellij.dev/ (modern alternative)

### Must-have CLI tools (replace old GNU)
- **ripgrep (rg)** — grep replacement
- **fd** — find replacement
- **bat** — cat replacement
- **eza** — ls replacement (formerly exa)
- **zoxide** — cd replacement
- **fzf** — fuzzy finder
- **delta** — better git diff
- **jq / yq / xq** — JSON/YAML/XML processors
- **httpie / curl** — HTTP clients
- **glow** — markdown renderer
- **gh** — GitHub CLI
- **tig** — TUI git
- **lazygit** — TUI git, easier
- **lazydocker** — TUI Docker
- **btop / htop** — process viewers
- **dust** — du replacement
- **duf** — df replacement
- **procs** — ps replacement
- **sd** — sed replacement

---

## Version Control

- **Git** — https://git-scm.com/
- **GitHub CLI (gh)** — https://cli.github.com/
- **lazygit** — https://github.com/jesseduffield/lazygit
- **GitKraken** — https://www.gitkraken.com/ (GUI)
- **Sublime Merge** — https://www.sublimemerge.com/ (GUI, fast)
- **Tower** — https://www.git-tower.com/ (macOS GUI)
- **GitHub Desktop** — https://desktop.github.com/ (beginner-friendly GUI)
- **git-secrets** — https://github.com/awslabs/git-secrets (prevent commit of secrets)
- **pre-commit** — https://pre-commit.com/ (manage hooks)

---

## Node.js / JS Runtimes & Package Managers

### Runtimes
- **Node.js** — https://nodejs.org/ (use 20 LTS or 22 LTS)
- **Bun** — https://bun.sh/
- **Deno** — https://deno.com/

### Version managers
- **nvm** — https://github.com/nvm-sh/nvm (Node)
- **fnm** — https://github.com/Schniz/fnm (faster nvm)
- **volta** — https://volta.sh/ (no shell config)
- **mise** — https://mise.jdx.dev/ (any language, asdf successor)
- **asdf** — https://asdf-vm.com/ (any language)

### Package managers
- **npm** — default
- **pnpm** — https://pnpm.io/ (fast, disk-efficient)
- **Yarn** — https://yarnpkg.com/ (Berry/v4+)
- **Bun** — built-in

### Build tools
- **Vite** — https://vitejs.dev/ (default for SPAs)
- **Turbopack** — https://turbo.build/pack (Next.js)
- **esbuild** — https://esbuild.github.io/ (low-level)
- **SWC** — https://swc.rs/ (Rust-based JS/TS compiler)
- **Rollup** — https://rollupjs.org/ (libraries)
- **Webpack** — https://webpack.js.org/ (legacy, still everywhere)
- **Bun.build** — built-in

### Linting / Formatting
- **ESLint** — https://eslint.org/
- **Biome** — https://biomejs.dev/ (Rust-based, fast, ESLint+Prettier replacement)
- **Prettier** — https://prettier.io/
- **dprint** — https://dprint.dev/ (Rust, multi-language)
- **Stylelint** — https://stylelint.io/ (CSS)
- **markdownlint** — https://github.com/DavidAnson/markdownlint
- **cspell** — https://cspell.org/

### Type checking
- **TypeScript** — https://www.typescriptlang.org/
- **tsc** — built-in
- **Astro Check** — for Astro
- **Vue SFC type-check** — `vue-tsc`

### Testing
- **Vitest** — https://vitest.dev/ (default for new projects)
- **Jest** — https://jestjs.io/ (legacy default)
- **Playwright** — https://playwright.dev/ (E2E)
- **Cypress** — https://www.cypress.io/ (E2E, alternative)
- **Testing Library** — https://testing-library.com/ (component tests)
- **MSW** — https://mswjs.io/ (mock service worker)
- **Storybook** — https://storybook.js.org/ (component dev)
- **Ladle** — https://ladle.dev/ (lighter Storybook)
- **Hurl** — https://hurl.dev/ (run curl-based tests)
- **k6** — https://k6.io/ (load testing)
- **Artillery** — https://www.artillery.io/ (load testing)

---

## Python

- **pyenv** / **mise** — version manager
- **uv** — https://github.com/astral-sh/uv (Astrally fast package manager; replaces pip + virtualenv)
- **Poetry** — https://python-poetry.org/ (popular alternative)
- **Ruff** — https://github.com/astral-sh/ruff (linter + formatter, replaces flake8+isort+black)
- **mypy** / **pyright** — type checkers
- **pytest** — testing
- **ipdb** / **pdb++** — debuggers
- **Jupyter** — https://jupyter.org/ (notebooks)
- **Marimo** — https://marimo.io/ (reactive notebooks)

---

## Go / Rust / Java / .NET / Ruby / PHP

### Go
- **Go** official installer
- **golangci-lint** — https://golangci-lint.run/
- **Delve** — debugger
- **Air** — https://github.com/cosmtrek/air (live reload)

### Rust
- **rustup** — https://rustup.rs/
- **cargo** — built-in
- **rust-analyzer** — LSP
- **clippy** — linter
- **rustfmt** — formatter

### Java
- **SDKMAN** — https://sdkman.io/ (version manager)
- **Maven** / **Gradle** — build tools
- **IntelliJ IDEA** — best IDE

### .NET
- **dotnet** SDK
- **Rider** (JetBrains) or VS Code with C# Dev Kit

### Ruby
- **rbenv** / **mise** — version manager
- **Bundler** — dependency management
- **RuboCop** — linter
- **Solargraph** — LSP

### PHP
- **Herd** (macOS) / **XAMPP** / **Docker**
- **Composer** — package manager
- **PHPStan** / **Psalm** — static analysis
- **Laravel Pint** — formatter (if Laravel)

---

## Database Tools

### SQL
- **TablePlus** — https://tableplus.com/ (best multi-DB GUI)
- **DBeaver** — https://dbeaver.io/ (free, cross-platform)
- **pgAdmin** — https://www.pgadmin.org/ (Postgres-specific, web)
- **DataGrip** — JetBrains
- **Postico** (macOS, Postgres)
- **Sequel Ace** (macOS, MySQL/MariaDB)
- **sqlite-studio** — https://github.com/frectonz/sqlite-studio (TUI)

### Document / Cache
- **MongoDB Compass** — https://www.mongodb.com/products/compass
- **Redis Insight** — https://redis.io/insight/

### ORM Studios
- **Prisma Studio** — https://www.prisma.io/studio
- **Drizzle Studio** — built into Drizzle Kit

### Migration Tools
- **Atlas** — https://atlasgo.io/ (declarative schema management)
- **Flyway** — https://flywaydb.org/
- **Liquibase** — https://www.liquibase.org/
- **Prisma Migrate** — built-in
- **node-pg-migrate** — https://github.com/salsita/node-pg-migrate

### Local DB spin-up
- **Docker Compose** — standard
- **Postgres.app** (macOS) — https://postgresapp.com/
- **DBngin** (macOS) — https://dbngin.com/
- **Nitro** / **Tilt** — local dev environments

---

## API Tools

- **Postman** — https://www.postman.com/
- **Insomnia** — https://insomnia.rest/
- **Bruno** — https://www.usebruno.com/ (open-source, Git-based)
- **Hoppscotch** — https://hoppscotch.io/ (web)
- **HTTPie** — https://httpie.io/ (CLI)
- **cURL** — built-in
- **jq** — https://stedolan.github.io/jq/
- **mitmproxy** — https://mitmproxy.org/ (intercept HTTPS)
- **HTTP Toolkit** — https://httptoolkit.com/ (friendlier mitm)
- **Paw / Rapid API** (macOS) — paid, very nice
- **MCP API testers** — emerging, see [MCP/](MCP/)

---

## Docker & Containers

- **Docker Desktop** — https://www.docker.com/products/docker-desktop/
- **OrbStack** (macOS, faster) — https://orbstack.dev/
- **Colima** (macOS, free) — https://github.com/abiosoft/colima
- **Rancher Desktop** — https://rancherdesktop.io/
- **Podman** — https://podman.io/ (daemonless)
- **lazydocker** — TUI
- **dive** — https://github.com/wagoodman/dive (inspect image layers)
- **trivy** — https://github.com/aquasecurity/trivy (image security scan)
- **hadolint** — https://github.com/hadolint/hadolint (Dockerfile linter)
- **docker-slim** — https://github.com/slimtoolkit/slim (shrink images)

---

## Kubernetes

- **kubectl** — https://kubernetes.io/docs/reference/kubectl/
- **k9s** — https://k9scli.io/ (TUI)
- **lens** — https://k8slens.dev/ (GUI)
- **kubectx / kubens** — https://github.com/ahmetb/kubectx
- **stern** — https://github.com/stern/stern (multi-pod logs)
- **helm** — https://helm.sh/
- **Argo CD** — https://argoproj.github.io/argo-cd/ (GitOps)
- **Flux** — https://fluxcd.io/ (GitOps)
- **kubebuilder** — https://book.kubebuilder.io/ (operator SDK)

---

## Cloud CLIs

- **AWS CLI v2** — https://aws.amazon.com/cli/
- **aws-vault** — https://github.com/99designs/aws-vault (creds management)
- **gcloud** — https://cloud.google.com/sdk/gcloud
- **az** — https://learn.microsoft.com/cli/azure/
- **vercel** — https://vercel.com/docs/cli
- **netlify** — https://docs.netlify.com/cli/get-started/
- **wrangler** (Cloudflare) — https://developers.cloudflare.com/workers/wrangler/
- **flyctl** (Fly.io) — https://fly.io/docs/hands-on/install-flyctl/
- **railway** CLI — https://railway.app/
- **render** CLI
- **supabase** CLI — https://supabase.com/docs/guides/cli
- **planetscale** CLI (note: hobby tier retired)
- **neon** CLI
- **turso** CLI
- **upstash** CLI

---

## CI/CD

- **GitHub Actions** — primary
- **GitLab CI** — if on GitLab
- **CircleCI** — alternative
- **Buildkite** — hybrid, fast
- **Drone** — open source
- **Woodpecker** — open source
- **act** — https://github.com/nektos/act (run Actions locally)
- **setup-node / setup-python etc.** — official actions

---

## Monitoring & Observability

- **OpenTelemetry** — https://opentelemetry.io/
- **Sentry** — https://sentry.io/ (errors)
- **Datadog** — https://www.datadoghq.com/
- **New Relic** — https://newrelic.com/
- **Grafana** — https://grafana.com/ (dashboards)
- **Prometheus** — https://prometheus.io/ (metrics)
- **Loki** — https://grafana.com/oss/loki/ (logs)
- **Tempo** — https://grafana.com/oss/tempo/ (traces)
- **Jaeger** — https://www.jaegertracing.io/ (traces)
- **LogRocket** — https://logrocket.com/ (session replay)
- **PostHog** — https://posthog.com/ (product analytics)
- **Plausible** — https://plausible.io/ (privacy analytics)
- **Umami** — https://umami.is/ (privacy analytics, self-hostable)
- **Axiom** — https://axiom.co/ (logs)
- **Highlight.io** — https://www.highlight.io/ (full-stack observability)

---

## Design & Prototyping

- **Figma** — https://www.figma.com/ (industry default)
- **Penpot** — https://penpot.app/ (open-source)
- **Sketch** — https://www.sketch.com/ (macOS)
- **Framer** — https://www.framer.com/ (design + ship)
- **Spline** — https://spline.design/ (3D)
- **Rive** — https://rive.app/ (animation, interactive)
- **Lottielab** — https://www.lottielab.com/ (Lottie animations)
- **Excalidraw** — https://excalidraw.com/ (hand-drawn diagrams)
- **tldraw** — https://www.tldraw.com/ (whiteboard)
- **Eraser** — https://www.eraser.io/ (diagrams)
- **Whimsical** — https://whimsical.com/
- **Balsamiq** — https://balsamiq.com/ (wireframes)
- **Mind npm** — https://www.mindmup.com/ (mind maps)

---

## Image & Media Editing

- **GIMP** — https://www.gimp.org/
- **Krita** — https://krita.org/ (digital painting)
- **Inkscape** — https://inkscape.org/ (SVG)
- **Affinity Photo / Designer / Publisher** — https://affinity.serif.com/
- **Pixelmator Pro** (macOS)
- **Squoosh** — https://squoosh.app/ (image compression)
- **SVGO** — https://github.com/svg/svgo (SVG optimization)
- **SVGOMG** — https://jakearchibald.github.io/svgomg/ (web UI)
- **ImageOptim** (macOS) — https://imageoptim.com/
- **FFmpeg** — https://ffmpeg.org/ (video)
- **HandBrake** — https://handbrake.fr/ (video transcode)
- **OBS Studio** — https://obsproject.com/ (recording/streaming)

---

## Productivity & Note-Taking

- **Obsidian** — https://obsidian.md/ (markdown notes, local)
- **Notion** — https://notion.so/
- **Linear** — https://linear.app/ (issue tracking)
- **GitHub Projects** — built-in
- **Jira** — https://www.atlassian.com/software/jira (enterprise default)
- **Todoist** — https://todoist.com/
- **Things 3** (macOS) — https://culturedcode.com/things/
- **Raycast** (macOS) — https://www.raycast.com/ (launcher)
- **Alfred** (macOS) — https://www.alfredapp.com/
- **Rectangle** / **Magnet** / **Moom** (macOS) — window management
- **Karabiner-Elements** (macOS) — keyboard customization

---

## AI Tools (for development)

- **Cursor** — https://cursor.sh/
- **Claude Code** — https://www.anthropic.com/news/claude-code
- **GitHub Copilot** — https://github.com/features/copilot
- **Continue** — https://www.continue.dev/ (open-source, in-editor)
- **Cline** — https://github.com/cline/cline (open-source agentic)
- **Aider** — https://aider.chat/ (CLI)
- **Codeium** — https://codeium.com/ (free tier)
- **Tabnine** — https://www.tabnine.com/
- **Sourcegraph Cody** — https://sourcegraph.com/cody
- **OpenHands** — https://github.com/All-Hands-AI/OpenHands
- **v0** — https://v0.dev/ (UI generation)
- **Bolt.new** — https://bolt.new/ (full-stack generation)
- **Replit Agent** — https://replit.com/
- **Lovable** — https://lovable.dev/

→ [Agentic-Coding/](Agentic-Coding/) for workflows.

---

## Security Tools

- **1Password / Bitwarden / KeePassXC** — password managers
- **OWASP ZAP** — https://www.zaproxy.org/
- **Burp Suite** — https://portswigger.net/burp
- **Snyk** — https://snyk.io/
- **Dependabot** — GitHub-native
- **Sigstore / cosign** — https://www.sigstore.dev/
- **trivy** — image/vuln scanning
- **grype** — https://github.com/anchore/grype
- **securityheaders.com** — https://securityheaders.com/
- **SSL Labs** — https://www.ssllabs.com/ssltest/
- **Mozilla Observatory** — https://observatory.mozilla.org/
- **dnsdumpster** — https://dnsdumpster.com/
- **Shodan** — https://www.shodan.io/ (search exposed devices)
- **Have I Been Pwned** — https://haveibeenpwned.com/

---

## Documentation

- **Mintlify** — https://mintlify.com/
- **Docusaurus** — https://docusaurus.io/
- **VitePress** — https://vitepress.dev/ (Vue-based)
- **Astro Starlight** — https://starlight.astro.build/
- **Nextra** — https://nextra.site/ (Next.js-based)
- **GitBook** — https://www.gitbook.com/
- **ReadMe** — https://readme.com/
- **Docsify** — https://docsify.js.org/
- **MkDocs** — https://www.mkdocs.org/ (Python)
- **Sphinx** — https://www.sphinx-doc.org/ (Python)
- **JSDoc / TSDoc** — code-level
- **TypeDoc** — https://typedoc.org/ (TS)
- **Storybook** — component docs

---

## Communication & Collaboration

- **Slack** — https://slack.com/
- **Discord** — https://discord.com/
- **Linear** — issues
- **Notion** — wiki
- **Confluence** — enterprise wiki
- **Loom** — https://www.loom.com/ (video)
- **Excalidraw** — diagrams
- **Miro** — https://miro.com/ (whiteboard)
- **FigJam** — Figma's whiteboard

---

## Setup Script (macOS, opinionated)

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install tools
brew install git gh node bun pnpm fnm ripgrep fd bat eza zoxide fzf jq delta starship tmux lazygit lazydocker k9s kubectx stern helm act httpie ffmpeg imagemagick

# Install apps
brew install --cask visual-studio-code cursor wezterm iterm2 tableplus docker postman obsidian raycast rectangle

# Setup shell
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
echo 'eval "$(zoxide init zsh)"' >> ~/.zshrc
echo 'eval "$(fnm env --use-on-cd)"' >> ~/.zshrc

# Git
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global core.pager delta
```

For Linux: same tools via your package manager. For Windows: use WSL2 + same as Linux.

---

## Sanity Check

After setup, you should be able to run:

```bash
node --version
bun --version
pnpm --version
git --version
gh --version
rg --version
fd --version
jq --version
docker --version
```

If all of these work, you're ready to build.

---

**Next:** [RESOURCES.md](RESOURCES.md) · [EXTERNAL_REPOSITORIES.md](EXTERNAL_REPOSITORIES.md) · [START-HERE.md](START-HERE.md)
