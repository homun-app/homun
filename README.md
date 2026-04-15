# Homun

**Your personal AI assistant. Single binary. Privacy-first. Local-first. Multi-channel.**

Homun is a digital homunculus that lives on your machine and works 24/7. Manage it from Telegram, WhatsApp, Discord, Slack, Email, a Web dashboard, or the CLI. It learns from you, runs automations while you sleep, browses the web, and extends via the open Agent Skills ecosystem.

> This is the **public face** of Homun — the home for issues, releases, discussions, and user-facing documentation.
>
> - 📦 **Source code**: private (`homun-app/homun-core`) under the [PolyForm Noncommercial License](https://polyformproject.org/licenses/noncommercial/1.0.0/). See [CONTRIBUTING](#contributing) below for security audit access.
> - 🌐 **Website**: [homun.dev](https://homun.dev)
> - 📋 **Changelog**: [CHANGELOG.md](https://github.com/homun-app/homun/blob/main/CHANGELOG.md)
> - 🚀 **Latest release**: [releases/latest](https://github.com/homun-app/homun/releases/latest)

---

## Quick install

### macOS

Download the latest `.dmg` from [GitHub Releases](https://github.com/homun-app/homun/releases/latest), drag `Homun.app` onto `Applications`, launch. The web dashboard opens at `http://localhost:8777`.

Or via **Homebrew**:

```bash
brew install homun-app/tap/homun
homun gateway
```

### Linux (Debian / Ubuntu)

```bash
curl -LO https://github.com/homun-app/homun/releases/latest/download/homun_1.0.0-1_amd64.deb
sudo apt install ./homun_1.0.0-1_amd64.deb
sudo -u homun homun gateway &
```

arm64 also available — substitute `amd64` with `arm64` in the URL.

### Linux (Fedora / RHEL / Rocky)

```bash
sudo dnf install https://github.com/homun-app/homun/releases/latest/download/homun-1.0.0-1.x86_64.rpm
sudo -u homun homun gateway &
```

### Windows (via WSL2)

Windows is supported via Windows Subsystem for Linux 2. Full walkthrough: **[docs/INSTALL-WINDOWS-WSL.md](https://github.com/homun-app/homun/blob/main/docs/INSTALL-WINDOWS-WSL.md)** (~15 minutes).

> A native Windows `.msi` installer is not provided in v1.0 — cost-driven rescope, see the changelog for details.

Once installed, open **http://localhost:8777** in your browser and complete the setup wizard.

---

## What you get

- **Multi-channel** — 7 channels: CLI, Telegram, WhatsApp, Discord, Slack, Email, Web WebSocket
- **14+ LLM providers** — Anthropic, OpenAI, Ollama (local), OpenRouter, DeepSeek, Groq, Gemini, Mistral, Together, Fireworks, and more
- **Long-term memory** — short-term session + long-term LLM-consolidated summaries, hybrid HNSW + FTS5 + RRF search
- **Knowledge base (RAG)** — ingest 30+ formats with vault-gating for sensitive data
- **23+ built-in tools** — shell, files, web search, browser automation, vault, email, scheduling, workflows, contacts
- **Automations** — visual flow builder (n8n-style SVG canvas), NLP flow generation
- **Workflow engine** — persistent multi-step workflows with approval gates and retry logic
- **Browser automation** — Playwright-powered headless browser, stealth injection, 21 unified actions
- **Skills ecosystem** — open Agent Skills standard, GitHub install, ClawHub marketplace
- **MCP integration** — connect external services via Model Context Protocol, OAuth + vault-resolved credentials
- **Security** — AES-256-GCM vault, 2FA TOTP, sandboxed execution (5 backends), exfiltration guard, emergency kill switch
- **Mobile app** — Flutter thread-first UX with inline approval blocks, biometric lock
- **Observability** — `/metrics` Prometheus endpoint, end-to-end X-Request-ID tracing, panic handler with redacted crash reports, daily update checker
- **Web dashboard** — 29 pages covering every aspect of the agent

---

## Documentation

- **[Changelog](./CHANGELOG.md)** — all notable changes
- **[Contributing](./CONTRIBUTING.md)** — how to report bugs and propose features
- **[Security policy](./SECURITY.md)** — vulnerability reporting
- **[homun.dev](https://homun.dev)** — project website with screenshots, guides, and community

---

## Contributing

Homun is **source-private, user-visible**:

- ✅ **Welcome**: bug reports, feature discussions, crash reports, documentation improvements
- ❌ **Not accepted**: public pull requests to the source (because there is no public source)
- 🔒 **Security audit access**: researchers can request read-only access to `homun-app/homun-core` — email `security@homun.app`

See [CONTRIBUTING.md](./CONTRIBUTING.md) for details. Read it before opening an issue or discussion so you know the license model.

---

## Report a bug

Use [GitHub Issues](https://github.com/homun-app/homun/issues/new/choose) — the templates guide you through the required fields.

For security vulnerabilities, **do not open public issues**. See [SECURITY.md](./SECURITY.md).

---

## Community

- 💬 [GitHub Discussions](https://github.com/homun-app/homun/discussions) — feature requests, Q&A, show-and-tell
- 🐛 [Issues](https://github.com/homun-app/homun/issues) — bug reports, crash reports
- 📣 [homun.dev](https://homun.dev) — announcements and release notes

---

## License

The documentation and templates in this public repository are released under the **MIT License** (see [LICENSE](./LICENSE)). This allows anyone to fork and adapt the docs freely.

The actual **source code** of Homun lives in the private `homun-app/homun-core` repository under the **[PolyForm Noncommercial License 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/)** — free for personal and non-commercial use.
