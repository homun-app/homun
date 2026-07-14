# Security Policy

## Report a vulnerability privately

Do not open a public issue for a security vulnerability.

- Use [GitHub Security Advisories](https://github.com/homun-app/homun/security/advisories/new), or
- email `security@homun.app`.

Include the affected Homun version, operating system, impact, minimal reproduction
steps, and whether the issue is already being exploited. Do not include credentials,
personal data, or an unreviewed diagnostic archive.

## Supported version

Security fixes target the latest release published in
[`homun-app/homun-releases`](https://github.com/homun-app/homun-releases/releases/latest).
Please reproduce the issue on the latest version when it is safe to do so.

## Scope

Reports are welcome for authorization bypasses, secret exposure, sandbox escapes,
unexpected tool execution, prompt-injection paths that cross an approval boundary,
arbitrary file access, cross-project data leakage, and other issues that can harm a
Homun user or their data.

The current source is public in
[`homun-core`](https://github.com/homun-app/homun-core) under the license in
[`LICENSE.md`](https://github.com/homun-app/homun-core/blob/main/LICENSE.md).

## Coordinated disclosure

Please allow time to investigate and publish a fix before sharing technical details
publicly. We will coordinate disclosure based on severity and user risk.
