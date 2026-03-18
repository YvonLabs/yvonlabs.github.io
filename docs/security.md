---
title: Security Policy
permalink: /docs/security
---

# Security Policy

YvonLabs welcomes responsible disclosure of security or privacy vulnerabilities across all its projects.

The workbench includes Chrome extensions, open source tools, and self-hosted software. Projects are built with a local-first, minimal-permissions philosophy. Most do not involve centralized servers or remote APIs.

---

### Supported versions

Security fixes apply to current stable releases and the active development branch (`main`). Older builds may continue to function but do not receive patches or dependency updates.

| Version | Supported | Notes |
|---------|-----------|-------|
| Current release | Active | Latest public release with all fixes |
| main | Active | In development, reviewed before publishing |
| Older versions | Limited | May work but not maintained |

Fixes land in `main` first, then are published as a patch release. Once published to the Chrome Web Store or deployed as a release, that version becomes the supported one.

---

### Projects

#### ToastKit

Chrome extension for targeted site resets. Clears cookies, cache, and storage for a single domain without affecting the rest of the browser.

Security scope:
- Handling of browser storage and cookie data within Chrome's sandboxed APIs
- Permission model scoped to `activeTab` and `browsingData`
- Injection or rendering of untrusted content in the popup
- No remote communication, no telemetry, no external dependencies

#### HeaderCheck

Chrome extension that evaluates HTTP response headers and produces a weighted privacy and security score using a deterministic scoring model (`SCM-2025.1`).

Security scope:
- All analysis occurs entirely within the user's browser context
- No remote communication or telemetry
- No API exposure beyond Chrome's declarative permissions
- Scoring logic reflects header configuration state only, not vulnerability severity
- Model results are static and auditable

#### IVAR

Open source threat intelligence dashboard. Self-hosted. Pulls from public feeds, triages signals using AI, and surfaces what matters for your stack.

Security scope:
- Injection or mishandling of untrusted feed content
- Authentication or access control issues in the FastAPI backend
- Exposure of sensitive configuration such as API keys or org profile data
- Vulnerabilities in Python or Node dependencies
- IVAR does not collect telemetry or operate shared cloud infrastructure

---

### General scope

Across all YvonLabs projects, security issues generally refer to:

- Handling of data within the user's local environment
- Permission or privilege misconfiguration
- Injection or rendering of untrusted content
- Violation of a project's defined local-only or read-only boundaries
- Logic that may misrepresent security or privacy state

---

### Reporting a vulnerability

Please do not open a public issue for potential security or privacy concerns.

Email: **237143566+yvon-l@users.noreply.github.com**

Include:
- Steps to reproduce
- Expected and actual behavior
- Environment details (browser, OS, or runtime version)
- Project name and version

Reports receive acknowledgment within 3 business days. Validated issues are prioritized and patched promptly.

---

### Disclosure and patch process

Validated fixes are released as patch versions and documented in release notes or changelogs. If a report results in a user-facing privacy or safety improvement it will be mentioned in the public release notes. Where applicable, model adjustments such as `SCM-2025.2` are versioned in `CHANGELOG.md` for transparency.

---

### Principles

- **Local-first:** computation and storage remain within the user's device where possible
- **Minimal permissions:** least privilege for Chrome, web, and server APIs
- **No telemetry:** no analytics, no tracking, no remote calls unless explicitly configured
- **Transparent changelog:** all changes including security patches are versioned and documented
- **Deterministic evaluation:** scoring models are static and auditable

---

<p align="center">
  <sub>Minimal · Fast · Focused © YvonLabs</sub>
</p>
