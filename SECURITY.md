# Security Policy

## Reporting a vulnerability

**Do not open public GitHub issues for security vulnerabilities.** Please use one of these private channels instead:

- 📧 **Email**: `security@homun.app` (PGP key: TBD — to be published with v1.0.1)
- 🔒 **GitHub Security Advisories**: [Open a new advisory](https://github.com/homun-app/homun/security/advisories/new)

We aim to respond within **5 business days**. Please include:

- A clear description of the vulnerability
- Steps to reproduce (minimal proof-of-concept if possible)
- Affected version(s) — check `homun --version` on your install
- OS and installer method (macOS `.dmg` / brew / Ubuntu `.deb` / Fedora `.rpm` / WSL)
- Your suggested severity (low / medium / high / critical)
- Whether you are willing to be credited in the fix announcement

## Coordinated disclosure

We prefer **coordinated disclosure**. Please give us a reasonable window — typically **30 days** — to ship a fix before publishing details publicly.

If the vulnerability is actively being exploited or puts users at immediate risk, we may ship an emergency hotfix with a shorter window. We'll coordinate the timeline with you.

## Supported versions

Only the **latest released version** receives security updates.

| Version | Supported |
|---|---|
| 1.0.x | ✅ Yes |
| 0.2.x and earlier | ❌ No — please upgrade |
| Pre-releases (`-rc`, `-beta`) | ❌ No |

## Security audit access (read-only source)

Homun's source code is **private** under the [PolyForm Noncommercial License 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/), not publicly open source. However, we grant **read-only access** to the private `homun-app/homun-core` repository for legitimate security research.

To request access, email `security@homun.app` with:

- Your identity and affiliation (individual / organization / company)
- Prior published audits or credentials (if any)
- Scope of the audit (full codebase / specific domain / specific version)
- Timeline and expected deliverables
- Willingness to follow coordinated disclosure

Decisions are made on a case-by-case basis. Responses typically arrive within 1 week.

## Existing internal audit surface

Before v1.0 shipped, **6 internal code audits** were conducted covering all 16 core domains, reviewing approximately ~41K LOC:

- Channels (Telegram, WhatsApp, Discord, Slack, Email, CLI, Web)
- Memory + RAG (vector search, ingestion, sensitive data handling)
- Security end-to-end (vault, exfiltration guard, auth, 2FA, e-stop, sandbox)
- Skills + MCP + Contacts + Profiles (identity isolation, OAuth, profile scoping)
- Automations + Workflow + Heartbeat (scheduling, approval gates, persistence)
- Observability (metrics, tracing, crash reports)

The audit findings (47 open bugs across 5 🔴 critical + 31 🟡 medium + 11 🟢 low) are documented in the private repository. Critical bugs with workarounds are listed in the public [CHANGELOG.md](./CHANGELOG.md) under "Known issues".

Security researchers with audit access can see the full findings including root cause analysis and fix priority.

## What is in-scope

Security reports are welcome for:

- **Authentication and authorization** — web auth, API keys, channel pairing, 2FA bypass
- **Vault and secrets management** — AES-256-GCM vault, keychain integration, vault leak detection
- **Sandbox escape** — from skill executors, tool shell commands, MCP subprocess, browser automation
- **Exfiltration** — PII / credentials / vault values leaking via channel outputs or logs
- **Prompt injection** — untrusted content escalating to tool calls the user did not authorize
- **Path traversal / arbitrary file access** — in `remember`, RAG ingest, file tools
- **Denial of service** — unbounded resource consumption (memory, file size, connections)
- **Profile isolation bypass** — cross-profile data leakage in multi-profile deployments
- **Injection via trace ID, HTTP headers, or crash report submission**

## What is out-of-scope

- **Bugs that are not security-relevant** — use regular issues or discussions
- **Social engineering against maintainers** — we respond to technical reports only
- **Rate limit bypass on publicly accessible Homun instances** — users are expected to configure rate limits appropriately
- **DoS requiring privileged access** — if you already have admin, you can already break things
- **Vulnerabilities in third-party dependencies** — please report to the upstream project first; we track via `cargo audit` and Dependabot

## Acknowledgments

Security researchers who help improve Homun will be credited in the fix announcement and the `CHANGELOG.md` (unless you prefer to remain anonymous).

There is **no bug bounty program** at this time. Homun is a single-maintainer project under a noncommercial license — we cannot offer monetary rewards, but we deeply appreciate responsible disclosure.

---

Thank you for helping keep Homun users safe.
