---
title: Security Policy
permalink: /docs/security
---

# Security Policy

YvonLabs welcomes responsible disclosure of security or privacy vulnerabilities across all its projects.

My workbench includes small, independent utilities, web tools, and browser-based software - typically client-side and local by design.  
There are no centralized production servers or remote APIs associated with most YvonLabs software.

---

### Supported Versions
Security fixes apply to current stable releases and the active development branch (`main`).  
Older builds may run but do not receive patches or dependency updates.

| Version | Supported | Notes |
|----------|------------|-------|
| **Current Release** | ✅ Active | Latest public release with all fixes and hardening |
| **main** | ✅ Active | In-development, verified before publishing |
| **Older versions** | ⚠︎ Limited | May work but not maintained |

Fixes land in `main` first, then are published as a patch release (for example, `0.2.2`).  
Once published to the Chrome Web Store or other platform, that becomes the supported version.

---

YvonLabs projects do not send, store, or process external data.  
Security issues generally refer to:  
- Handling of data within the user’s local environment (browser, extension sandbox, or OS scope)  
- Permission or privilege misconfiguration  
- Injection or rendering of untrusted content  
- Violation of a project’s defined **local-only** or **read-only** boundaries  
- Scoring or evaluation logic that may misrepresent a site’s security or privacy headers

---

### HeaderCheck Model Context  

**HeaderCheck** uses a deterministic scoring model (`SCM-2025.1`) that evaluates HTTP response headers locally.  
The model does not involve live scanning or external calls.  
All analysis and computation occur entirely within the user’s browser context.  

**Security implications:**  
- No remote communication or telemetry  
- No API exposure beyond Chrome’s declarative permissions  
- Scoring logic cannot exfiltrate or transmit content  
- Model results reflect header configuration state only — not vulnerability severity

---

### Reporting a Vulnerability
Please do **not** open a public issue for potential security or privacy concerns.  
Instead, email:  
**237143566+yvon-l@users.noreply.github.com**

Include:
- Steps to reproduce  
- Expected and actual behavior  
- Environment details (browser, OS, or runtime)  
- Project and version information  

Reports receive acknowledgment within **3 business days**, and validated issues are prioritized.

---

### Disclosure & Patch Process
Validated fixes are released as patch versions and publicly documented in release notes or changelogs.  
If a report results in a user-facing privacy or safety improvement, it will be mentioned in the public release notes.  
Where applicable, model adjustments (for example, `SCM-2025.2`) are versioned in `CHANGELOG.md` for transparency.
---

### Principles  
- **Local-first:** all computation and storage remain within the user’s device  
- **Minimal permissions:** least privilege for Chrome or web APIs  
- **No telemetry:** no analytics, no tracking, no remote calls  
- **Transparent changelog:** all changes, including security patches, are versioned  
- **Deterministic evaluation:** models (like HeaderCheck SCM-2025.1) are static and auditable   

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
