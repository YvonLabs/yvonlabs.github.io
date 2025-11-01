# ToastKit  

**Type:** Chrome Extension  
**Maintained by:** YvonLabs  
**Current Release:** v0.2.1  
**Last Updated:** November 1, 2025  

---

### Overview  

ToastKit is a privacy-first Chrome extension that resets cookies, cache, and storage for a **single site** without clearing your entire browser.  
It was designed for developers, QA engineers, and privacy-conscious users who need a clean slate per domain — fast, contained, and transparent.  

All processing occurs **locally** within the browser’s sandbox. No telemetry, tracking, or remote calls are used.

---

### Key Features  

- **Targeted reset** – clear data only for the current site or domain.  
- **Granular control** – choose which elements to clear: cookies, cache, local or session storage.  
- **Instant feedback** – see confirmation in the popup after each action.  
- **Keyboard shortcut** – press **Alt + T** to reset the current site instantly.  
- **Minimal design** – lightweight UI, zero background activity when idle.  

---

### Privacy  

ToastKit operates completely on-device.  
It does **not** collect telemetry, analytics, or any user data.  
All functions run via Chrome’s built-in privacy APIs, with no external network communication.  

For global privacy commitments across all YvonLabs projects, see the  
[Unified Privacy Policy](https://yvonlabs.github.io/docs/privacy-policy).

---

### Security  

ToastKit follows the [YvonLabs Security Policy](https://yvonlabs.github.io/docs/security), which includes:  
- **Local-only computation** – no remote endpoints or dependencies  
- **Minimal permissions model** – scoped to activeTab and browsingData  
- **Static review and version control before release**  
- **Transparent changelog and version tracking**

---

### Supported Versions  

| Version | Status | Notes |
|----------|---------|-------|
| **0.2.1** | ✅ Active | Latest hardening release (DOM sanitization, popup safety) |
| **main** | ✅ Active | Development branch — reviewed before publishing |
| **0.2.0** | ⚠️ Superseded | Replaced by 0.2.1 for security reasons |
| **≤ 0.1.x** | ❌ Unsupported | Internal builds, not maintained |

---

### Versioning  

- Binary release: **v0.2.1**  
- Future versions documented in [CHANGELOG.md](https://github.com/YvonLabs/toastkit/blob/main/CHANGELOG.md)  
- Once a new version is submitted and approved in the Chrome Web Store, it becomes the supported version.  

---

### Repository  

For installation instructions, issues, or contributions, visit:  
👉 [ToastKit on GitHub](https://github.com/YvonLabs/toastkit)

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
