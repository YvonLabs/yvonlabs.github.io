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

### What a “Security Issue” Means Here
YvonLabs projects do not collect data or communicate externally.  
Security issues generally refer to:
- Handling of data within the user’s browser or environment  
- Permission or privilege misconfiguration  
- Injection or rendering of untrusted content  
- Violations of a project’s defined local-only scope  

---

### Reporting a Vulnerability
Please do **not** open a public issue for security or privacy concerns.  
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

---

### Principles
- Minimal permissions and local execution  
- No telemetry, tracking, or analytics  
- Transparent changelog and release tagging  

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
