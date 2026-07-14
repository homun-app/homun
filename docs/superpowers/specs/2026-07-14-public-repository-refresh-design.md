# Homun Public Repository Refresh Design

**Date:** 2026-07-14
**Status:** Approved direction, pending written-spec review

## Goal

Make `homun-app/homun` the accurate public entry point for the Homun product:
product orientation, downloads, community ideas, bug and crash reports, security
contact, and repository navigation.

The repository must stop presenting the retired gateway-first product as the current
desktop application. Public claims must match the website, the current desktop code,
the current release repository, and the current source license.

## Current problems

- The README, contribution guide, security policy, issue forms, repository description,
  and changelog describe the former single-binary gateway product.
- Links point to `homun.dev`, which now redirects to another site.
- Downloads point to legacy `homun` releases instead of
  `homun-app/homun-releases`.
- Several files describe `homun-core` as private and PolyForm-licensed; it is public
  and currently uses FSL-1.1-ALv2.
- Bug and crash forms request obsolete commands, installers, paths, and dashboard
  behavior.
- The new roadmap idea form exists, but the `idea` label is absent and the chooser
  still sends feature requests to Discussions.
- The repository metadata still says “Single binary” and has no homepage.

## Approaches considered

### 1. Patch links only

Update domains and release URLs while preserving the existing documents.

This is low effort but rejected: most product, installation, contribution, and
security claims would remain wrong.

### 2. Full public-hub refresh

Rewrite the public-facing files around the current desktop product, keep useful
support boundaries, and replace stale duplicated history with canonical links.

This is the selected approach. It gives the repository one durable responsibility
without duplicating source documentation or release history.

### 3. Archive `homun` and route everything to `homun-core`

This would reduce repository count but mix product ideas, user support, and technical
implementation work. It is rejected because the roadmap requires one product-level
community intake that can route work to multiple repositories.

## Repository responsibility

`homun-app/homun` owns:

- the public product and community landing page;
- structured product-idea submission;
- public bug and crash intake;
- security reporting directions;
- navigation to the website, roadmap, documentation, source, and releases.

It does not own:

- application source or engineering documentation, which live in `homun-core`;
- installers and updater metadata, which live in `homun-releases`;
- the full changelog and user guides, which live on `homun.app`;
- internal engineering roadmaps.

## File design

### `README.md`

Rewrite as a concise product/community landing page:

1. current Homun positioning from the website;
2. website, documentation, roadmap, source, and download links;
3. a short explanation of local-first ownership and user control;
4. supported desktop platforms without hard-coded release versions;
5. clear calls to report a bug, suggest an idea, join Discussions, and report a
   vulnerability;
6. repository map for `homun`, `homun-core`, `homun-releases`, and `website`;
7. a short note that legacy releases in this repository are historical.

Avoid exhaustive feature counts, provider counts, architecture internals, future
promises, and version-specific installer filenames.

### `CONTRIBUTING.md`

Replace the private-source contribution model with the current public-source model:

- product ideas use the structured GitHub issue form;
- bugs and crashes use their issue forms;
- general questions use Discussions;
- source changes belong in `homun-core`;
- website changes belong in `website`;
- security reports use private channels;
- all participation follows a compact conduct boundary.

Do not promise response times, release cadence, audit access, or bounty availability.

### `SECURITY.md`

Keep a short, operational policy:

- never report vulnerabilities in public issues;
- use GitHub Security Advisories or `security@homun.app`;
- request reproduction steps, affected current version, impact, and environment;
- state that support applies to the latest release from `homun-releases`;
- link to the public source and its actual license.

Remove obsolete version tables, private-source access procedures, old audit counts,
known-critical-bug lists, PGP placeholders, and retired architecture details.

### `CHANGELOG.md`

Replace the duplicated legacy v1 changelog with a compact history pointer:

- current changelog: `https://homun.app/changelog`;
- current releases: `homun-app/homun-releases`;
- legacy v1 releases remain available in this repository for historical reference.

The file remains so links embedded in legacy release notes do not become 404s.

### `LICENSE`

Keep the standard MIT license for the documentation and issue-template content in
this repository. Remove the stale custom note that claims the source is private and
PolyForm-licensed. Explain repository boundaries and link the current source license
from the README instead of modifying the license text.

### `.github/ISSUE_TEMPLATE/roadmap-idea.yml`

Keep the approved moderated form. Retain the advisory-vote and no-delivery-commitment
language. Ensure the repository has an `idea` label.

### `.github/ISSUE_TEMPLATE/config.yml`

- keep blank issues disabled;
- rename the combined feature/general contact to general questions and community
  discussion only;
- keep the private security contact;
- update documentation to `https://homun.app/docs`.

Product ideas must use the structured issue form, not the generic Discussion contact.

### `.github/ISSUE_TEMPLATE/bug.yml`

Rewrite for the Electron desktop application:

- actual and expected behavior;
- reproducible steps;
- version visible in Settings;
- macOS, Windows, Linux, and other;
- installer type matching current release assets;
- optional diagnostic archive created from Settings → Report a problem;
- explicit reminder to review and redact paths or message fragments before upload.

Remove CLI, gateway, port 8777, WSL2, Homebrew, RPM, trace-ID, and old log-command
instructions.

### `.github/ISSUE_TEMPLATE/crash.yml`

Keep a separate crash intake because crashes need frequency and last-action context.
Rewrite it around the current local feedback bundle:

- version and platform;
- action immediately before the crash;
- reproducibility/frequency;
- optional archive from Settings → Report a problem;
- explicit review/redaction reminder.

Do not claim the app creates `~/.homun/crashes/*.json` or pre-fills GitHub issues.

## Repository settings

Update through GitHub after file validation:

- description: current local-first desktop product positioning;
- homepage: `https://homun.app`;
- create labels `idea`, `triage`, and `crash` with distinct descriptions/colors;
- preserve Issues, Discussions, and Security Advisories;
- do not delete or rewrite published legacy GitHub releases.

## Validation

Before publication:

1. parse every issue-template YAML file;
2. validate required issue-form keys and unique field identifiers;
3. confirm every referenced label exists;
4. scan tracked text for obsolete claims and links:
   `homun.dev`, private `homun-core`, PolyForm, `homun gateway`, port 8777,
   WSL2, `~/.homun/crashes`, and current downloads in `homun/releases`;
5. confirm all canonical HTTPS links respond or point to existing GitHub resources;
6. run `git diff --check`;
7. inspect the GitHub issue chooser after the branch is published.

## Publication

Commit the refresh on `fabio/public-repo-refresh`, push it, and open a draft Pull
Request against `main`. Repository metadata and labels may be updated directly
because they cannot be represented in the PR; perform them only after file validation
and report them separately.

The website should not be deployed with the idea-submission link until the template
is present on the default branch. The template already exists on `main`, so this
refresh does not block the current link.

## Success criteria

- A new visitor understands the current desktop product and where to download it.
- Product ideas, bugs, crashes, questions, and vulnerabilities each have one accurate
  destination.
- No public file claims that `homun-core` is private or PolyForm-licensed.
- No current installation guidance points to the retired gateway or legacy releases.
- Legacy release links remain valid without presenting legacy v1 as current.
- Repository labels, chooser configuration, and issue forms agree with each other.
