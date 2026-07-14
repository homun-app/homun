# Homun Public Repository Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox syntax for tracking.

**Goal:** Turn homun-app/homun into an accurate public product and community hub for the current Homun desktop application.

**Architecture:** Keep this repository intentionally small: concise product orientation, canonical links, moderated GitHub intake, and no duplicated source or release documentation. Validate through YAML parsing, semantic text contracts, live links, and repository-label checks before opening a draft PR.

**Tech Stack:** Markdown, GitHub Issue Forms YAML, Ruby YAML parser, ripgrep, GitHub CLI, git.

---

### Task 1: Establish the failing repository contract

**Files:**
- Read: README.md
- Read: CONTRIBUTING.md
- Read: SECURITY.md
- Read: CHANGELOG.md
- Read: .github/ISSUE_TEMPLATE/*.yml

- [ ] **Step 1: Prove obsolete product language is present**

Run:

~~~bash
rg -n "homun\.dev|private .*homun-core|PRIVATE repository|PolyForm|homun gateway|localhost:8777|WSL2|~/.homun/crashes|homun --version" README.md CONTRIBUTING.md SECURITY.md CHANGELOG.md .github/ISSUE_TEMPLATE
~~~

Expected: matches in the public documents and support forms.

- [ ] **Step 2: Prove the required labels are absent**

Run:

~~~bash
gh api 'repos/homun-app/homun/labels?per_page=100' --paginate --jq '.[].name' | sort > /tmp/homun-public-labels.txt
for label in idea triage crash; do
  grep -Fxq "$label" /tmp/homun-public-labels.txt || echo "missing $label"
done
~~~

Expected:

~~~text
missing idea
missing triage
missing crash
~~~

### Task 2: Rewrite README.md

**Files:**
- Modify: README.md

- [ ] **Step 1: Replace the README**

Use this complete content:

~~~markdown
# Homun

**Your work. Your models. Your system.**

Homun is a local-first desktop assistant that helps you work across conversations,
files, tools, automations, and connected services while keeping you in control of
what it can access and do.

[Website](https://homun.app) ·
[Documentation](https://homun.app/docs) ·
[Roadmap](https://homun.app/roadmap) ·
[Download](https://github.com/homun-app/homun-releases/releases/latest) ·
[Source](https://github.com/homun-app/homun-core)

## Why Homun

- **Local-first ownership** — your data and working context stay on your machine by default.
- **Your choice of models** — use local, open-source, or cloud providers.
- **Controlled action** — tools, connectors, and automations operate through explicit permissions.
- **Visible work** — follow plans, tool use, and progress while Homun works.

## Download

Current installers are published in
[homun-app/homun-releases](https://github.com/homun-app/homun-releases/releases/latest).

- macOS: Apple Silicon .dmg
- Windows: x64 .exe
- Linux: x86_64 .AppImage or amd64 .deb

See the [download guide](https://homun.app/guides/download/) for current platform
requirements and installation steps.

## Community

- [Suggest a product idea](https://github.com/homun-app/homun/issues/new?template=roadmap-idea.yml)
- [Report a bug or crash](https://github.com/homun-app/homun/issues/new/choose)
- [Ask a question or start a discussion](https://github.com/homun-app/homun/discussions)
- [Report a security vulnerability privately](./SECURITY.md)

Ideas are reviewed before they appear on the public roadmap. Voting opens on accepted
ideas with a public GitHub issue, and votes remain advisory.

## Repository map

| Repository | Responsibility |
| --- | --- |
| [homun](https://github.com/homun-app/homun) | Public product, community ideas, support, and security intake |
| [homun-core](https://github.com/homun-app/homun-core) | Desktop application source and engineering work |
| [homun-releases](https://github.com/homun-app/homun-releases) | Installers, updater metadata, and published releases |
| [website](https://github.com/homun-app/website) | Website, public documentation, roadmap, and changelog |

## Legacy releases

The v1.0.x releases stored in this repository belong to an earlier Homun architecture
and remain available for historical reference. Current desktop releases are published
only in [homun-app/homun-releases](https://github.com/homun-app/homun-releases/releases).

## License

The documentation and GitHub templates in this repository use the [MIT License](./LICENSE).
The Homun source code has its own license in
[homun-core/LICENSE.md](https://github.com/homun-app/homun-core/blob/main/LICENSE.md).
~~~

- [ ] **Step 2: Verify and commit**

Run:

~~~bash
rg -n "Your work\. Your models\. Your system\.|homun-releases/releases/latest|Repository map|Legacy releases|roadmap-idea.yml" README.md
git diff --check
git add README.md
git commit -m "docs: refresh the public Homun landing page"
~~~

Expected: all five boundaries found and a clean commit.

### Task 3: Rewrite public policies and history

**Files:**
- Modify: CONTRIBUTING.md
- Modify: SECURITY.md
- Modify: CHANGELOG.md
- Modify: LICENSE

- [ ] **Step 1: Replace CONTRIBUTING.md**

Use this complete content:

~~~markdown
# Contributing to Homun

Thanks for helping improve Homun. Choose the route that matches what you want to contribute.

| Contribution | Where it belongs |
| --- | --- |
| Product idea | [Structured idea form](https://github.com/homun-app/homun/issues/new?template=roadmap-idea.yml) |
| Bug or crash | [Issue chooser](https://github.com/homun-app/homun/issues/new/choose) |
| General question | [GitHub Discussions](https://github.com/homun-app/homun/discussions) |
| Desktop source change | [homun-core](https://github.com/homun-app/homun-core) |
| Website or public documentation | [website](https://github.com/homun-app/website) |
| Security vulnerability | [Private security reporting](./SECURITY.md) |

## Product ideas

Describe the user problem and the outcome that would become easier or possible.
Search existing issues first. Ideas are moderated before publication, may be merged
or archived, and do not become delivery commitments through vote totals.

## Bug and crash reports

Include reproducible steps, expected and actual behavior, the version shown in
Settings, and your operating system. Homun can create a local diagnostic archive from
Settings → Report a problem. Review it before attaching it because technical logs may
contain file paths or message fragments.

## Source and website contributions

Application code changes belong in homun-core; website and public-guide changes belong
in website. Check the target repository's current files and tests before opening a
pull request.

## Participation

Be concrete, respectful, and patient. Do not publish credentials, personal data, or
another person's private information. Maintainers may close duplicates, unsupported
requests, or disruptive discussions with an explanation.
~~~

- [ ] **Step 2: Replace SECURITY.md**

Use this complete content:

~~~markdown
# Security Policy

## Report a vulnerability privately

Do not open a public issue for a security vulnerability.

- Use [GitHub Security Advisories](https://github.com/homun-app/homun/security/advisories/new), or
- email security@homun.app.

Include the affected Homun version, operating system, impact, minimal reproduction
steps, and whether the issue is already being exploited. Do not include credentials,
personal data, or an unreviewed diagnostic archive.

## Supported version

Security fixes target the latest release published in
[homun-app/homun-releases](https://github.com/homun-app/homun-releases/releases/latest).
Please reproduce the issue on the latest version when it is safe to do so.

## Scope

Reports are welcome for authorization bypasses, secret exposure, sandbox escapes,
unexpected tool execution, prompt-injection paths that cross an approval boundary,
arbitrary file access, cross-project data leakage, and other issues that can harm a
Homun user or their data.

The current source is public in
[homun-core](https://github.com/homun-app/homun-core) under the license in
[LICENSE.md](https://github.com/homun-app/homun-core/blob/main/LICENSE.md).

## Coordinated disclosure

Please allow time to investigate and publish a fix before sharing technical details
publicly. We will coordinate disclosure based on severity and user risk.
~~~

- [ ] **Step 3: Replace CHANGELOG.md**

Use:

~~~markdown
# Changelog

The current Homun changelog is published at
[homun.app/changelog](https://homun.app/changelog).

Current installers and release notes are available from
[homun-app/homun-releases](https://github.com/homun-app/homun-releases/releases).

The v1.0.x releases in this repository document an earlier Homun architecture and
remain available under this repository's
[GitHub Releases](https://github.com/homun-app/homun/releases) for historical reference.
~~~

- [ ] **Step 4: Restore LICENSE to standard MIT**

Keep the MIT license through the warranty disclaimer. Delete the custom note after it;
source licensing is linked from the README.

- [ ] **Step 5: Verify and commit**

Run:

~~~bash
rg -n "Structured idea form|Settings → Report a problem|homun-releases" CONTRIBUTING.md
rg -n "security@homun.app|security/advisories/new|latest release|homun-core/blob/main/LICENSE.md" SECURITY.md
test "$(wc -l < CHANGELOG.md | tr -d ' ')" -lt 20
git diff --check
git add CONTRIBUTING.md SECURITY.md CHANGELOG.md LICENSE
git commit -m "docs: align public policies with the desktop app"
~~~

Expected: contracts found, compact changelog, clean commit.

### Task 4: Rewrite GitHub intake forms

**Files:**
- Modify: .github/ISSUE_TEMPLATE/bug.yml
- Modify: .github/ISSUE_TEMPLATE/crash.yml
- Modify: .github/ISSUE_TEMPLATE/config.yml
- Verify: .github/ISSUE_TEMPLATE/roadmap-idea.yml

- [ ] **Step 1: Update config.yml**

Use:

~~~yaml
blank_issues_enabled: false
contact_links:
  - name: 💬 General question or community discussion
    url: https://github.com/homun-app/homun/discussions
    about: Ask for help, share how you use Homun, or discuss a topic that is not a product proposal.
  - name: 🔒 Security vulnerability
    url: https://github.com/homun-app/homun/security/advisories/new
    about: Do not open public issues for vulnerabilities. Use a private advisory or email security@homun.app.
  - name: 📖 Documentation and usage help
    url: https://homun.app/docs
    about: Read current installation guides, product documentation, and reference material.
~~~

- [ ] **Step 2: Rewrite bug.yml**

Use:

~~~yaml
name: 🐛 Bug report
description: Something in the Homun desktop app is not working as expected
labels: ["bug", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for reporting a problem. Search existing issues first and do not include credentials or private data.
  - type: textarea
    id: description
    attributes:
      label: What happened?
      description: Briefly describe the problem.
    validations:
      required: true
  - type: textarea
    id: steps
    attributes:
      label: Steps to reproduce
      placeholder: |
        1. Open...
        2. Choose...
        3. Observe...
    validations:
      required: true
  - type: textarea
    id: expected
    attributes:
      label: Expected behavior
    validations:
      required: true
  - type: textarea
    id: actual
    attributes:
      label: Actual behavior
    validations:
      required: true
  - type: input
    id: version
    attributes:
      label: Homun version
      description: Find it in Settings → About & version.
      placeholder: Copy the exact version shown in Settings
    validations:
      required: true
  - type: dropdown
    id: os
    attributes:
      label: Operating system
      options:
        - macOS
        - Windows
        - Linux
        - Other
    validations:
      required: true
  - type: dropdown
    id: installer
    attributes:
      label: Installation package
      options:
        - macOS .dmg
        - Windows .exe
        - Linux .AppImage
        - Linux .deb
        - Other
    validations:
      required: true
  - type: textarea
    id: diagnostics
    attributes:
      label: Diagnostic archive (optional)
      description: |
        In Homun, open Settings → Report a problem and create the archive. Review it before attaching it: technical logs may contain file paths or message fragments. Redact anything you do not want to publish, then drag the archive here.
  - type: textarea
    id: context
    attributes:
      label: Additional context
      description: Add screenshots or other details that help reproduce the problem.
  - type: checkboxes
    id: checks
    attributes:
      label: Before submitting
      options:
        - label: I searched existing issues and did not find the same problem.
          required: true
        - label: I am using the latest released version, or I identified the exact older version above.
          required: true
        - label: I reviewed attachments and removed credentials and private data.
          required: true
~~~

- [ ] **Step 3: Rewrite crash.yml**

Use:

~~~yaml
name: 💥 Crash report
description: The Homun desktop app closed or its local engine stopped unexpectedly
labels: ["bug", "crash", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for reporting a crash. Do not include credentials or private data in public attachments.
  - type: textarea
    id: what_happened
    attributes:
      label: What were you doing immediately before the crash?
      description: Describe the last visible action and what closed or stopped.
    validations:
      required: true
  - type: dropdown
    id: frequency
    attributes:
      label: Can you reproduce it?
      options:
        - It happened once
        - It happens occasionally
        - It happens frequently
        - It happens every time with these steps
    validations:
      required: true
  - type: input
    id: version
    attributes:
      label: Homun version
      description: Find it in Settings → About & version.
      placeholder: Copy the exact version shown in Settings
    validations:
      required: true
  - type: dropdown
    id: os
    attributes:
      label: Operating system
      options:
        - macOS
        - Windows
        - Linux
        - Other
    validations:
      required: true
  - type: textarea
    id: diagnostics
    attributes:
      label: Diagnostic archive (optional)
      description: |
        Restart Homun if possible, open Settings → Report a problem, and create the archive. Review it before attaching it: technical logs may contain file paths or message fragments. Redact anything you do not want to publish, then drag the archive here.
  - type: textarea
    id: context
    attributes:
      label: Additional context
      description: Add reproduction steps, screenshots, or related errors.
  - type: checkboxes
    id: checks
    attributes:
      label: Before submitting
      options:
        - label: I searched existing issues and did not find the same crash.
          required: true
        - label: I reviewed attachments and removed credentials and private data.
          required: true
~~~

- [ ] **Step 4: Parse, verify, and commit**

Run:

~~~bash
ruby -e 'require "yaml"; Dir[".github/ISSUE_TEMPLATE/*.{yml,yaml}"].each { |f| YAML.load_file(f); puts "valid #{f}" }'
rg -n "Settings → Report a problem|message fragments" .github/ISSUE_TEMPLATE/bug.yml .github/ISSUE_TEMPLATE/crash.yml
rg -n "Votes are advisory|id: problem|id: value|id: area" .github/ISSUE_TEMPLATE/roadmap-idea.yml
git diff --check
git add .github/ISSUE_TEMPLATE
git commit -m "docs: update public support forms"
~~~

Expected: four valid YAML files, current diagnostics guidance, and unchanged roadmap semantics.

### Task 5: Complete repository validation and remove internal artifacts

**Files:**
- Delete: docs/superpowers/specs/2026-07-14-public-repository-refresh-design.md
- Delete: docs/superpowers/plans/2026-07-14-public-repository-refresh.md

- [ ] **Step 1: Run the obsolete-language scan**

Run:

~~~bash
if rg -n "homun\.dev|private .*homun-core|PRIVATE repository|PolyForm|homun gateway|localhost:8777|WSL2|~/.homun/crashes|homun --version" README.md CONTRIBUTING.md SECURITY.md CHANGELOG.md .github/ISSUE_TEMPLATE; then
  exit 1
fi
~~~

Expected: exit 0 with no matches.

- [ ] **Step 2: Check canonical links**

Run:

~~~bash
for url in https://homun.app https://homun.app/docs https://homun.app/roadmap https://homun.app/changelog https://github.com/homun-app/homun-core https://github.com/homun-app/homun-releases/releases/latest; do
  curl -fsSIL --max-time 15 "$url" >/dev/null || exit 1
done
~~~

Expected: exit 0.

- [ ] **Step 3: Remove planning documents and verify**

Delete docs/superpowers. Then run:

~~~bash
ruby -e 'require "yaml"; Dir[".github/ISSUE_TEMPLATE/*.{yml,yaml}"].each { |f| YAML.load_file(f) }'
git diff main...HEAD --check
git status --short
~~~

Expected: only the intended public files are modified and no untracked files remain after staging.

- [ ] **Step 4: Commit**

~~~bash
git add -A docs
git commit -m "chore: keep the public repository focused"
~~~

### Task 6: Publish and align GitHub settings

**Files:**
- No repository file changes

- [ ] **Step 1: Push**

~~~bash
git push -u origin fabio/public-repo-refresh
~~~

- [ ] **Step 2: Create labels**

~~~bash
gh label create idea --repo homun-app/homun --color 7C3AED --description "Community product idea under roadmap moderation"
gh label create triage --repo homun-app/homun --color FBCA04 --description "Needs maintainer review and routing"
gh label create crash --repo homun-app/homun --color B60205 --description "Application crash report"
~~~

- [ ] **Step 3: Update metadata**

~~~bash
gh repo edit homun-app/homun --description "Homun — a local-first personal assistant. Your work, your models, your system." --homepage "https://homun.app"
~~~

- [ ] **Step 4: Open a draft PR**

Create a draft PR from fabio/public-repo-refresh to main titled
"Refresh the public Homun repository". Its body covers the product rewrite, support
forms, legacy boundary, license correction, and verification evidence.

- [ ] **Step 5: Verify remote state**

Run:

~~~bash
gh api repos/homun-app/homun --jq '{description,homepage,has_issues,has_discussions}'
gh api 'repos/homun-app/homun/labels?per_page=100' --paginate --jq '.[].name' | grep -E '^(idea|triage|crash)$' | sort
gh pr view --repo homun-app/homun --json number,url,isDraft,headRefName,baseRefName
~~~

Expected: current metadata, all three labels, and one draft PR to main.
