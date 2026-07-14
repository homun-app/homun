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

- macOS: Apple Silicon `.dmg`
- Windows: x64 `.exe`
- Linux: x86_64 `.AppImage` or amd64 `.deb`

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
| [`homun`](https://github.com/homun-app/homun) | Public product, community ideas, support, and security intake |
| [`homun-core`](https://github.com/homun-app/homun-core) | Desktop application source and engineering work |
| [`homun-releases`](https://github.com/homun-app/homun-releases) | Installers, updater metadata, and published releases |
| [`website`](https://github.com/homun-app/website) | Website, public documentation, roadmap, and changelog |

## Legacy releases

The `v1.0.x` releases stored in this repository belong to an earlier Homun architecture
and remain available for historical reference. Current desktop releases are published
only in [`homun-app/homun-releases`](https://github.com/homun-app/homun-releases/releases).

## License

The documentation and GitHub templates in this repository use the [MIT License](./LICENSE).
The Homun source code has its own license in
[`homun-core/LICENSE.md`](https://github.com/homun-app/homun-core/blob/main/LICENSE.md).
