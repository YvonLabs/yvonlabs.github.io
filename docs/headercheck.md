# HeaderCheck  

**Type:** Chrome Extension  
**Maintained by:** YvonLabs  
**Current Model:** `SCM-2025.1`  
**Last Updated:** November 28, 2025  

---

### Overview  

HeaderCheck is a lightweight, privacy-respecting browser extension that inspects HTTP response headers for the active tab and evaluates the site's security and privacy posture.

It uses a deterministic, weighted scoring model to calculate a composite score from **0–100**, based on the presence and validity of key security headers.  
All processing occurs **locally in the browser** with no telemetry, network calls, or data collection.

---

### What HeaderCheck Evaluates  

HeaderCheck analyzes the most impactful modern browser security controls:

| Header / Control | Purpose |
|------------------|----------|
| **Strict-Transport-Security** | Prevents downgrade attacks and enforces secure transport |
| **Content-Security-Policy** | Primary defense against XSS and injection |
| **COOP / COEP / CORP** | Cross-origin and isolation boundaries |
| **Permissions-Policy** | Restricts high-risk browser APIs |
| **Referrer-Policy** | Minimizes referrer leakage |
| **X-Frame-Options / frame-ancestors** | Clickjacking protection |
| **X-Content-Type-Options (nosniff)** | Prevents MIME sniffing |

Headers are categorized as **graded** or **informational**.  
Only graded headers impact the score.

---

### Scoring Model  

HeaderCheck uses a weighted model totaling **10.0** raw points, normalized to **100**.

| Header | Weight |
|--------|---------|
| Content-Security-Policy | 2.0 |
| Strict-Transport-Security | 2.0 |
| COOP | 1.0 |
| COEP | 1.0 |
| CORP | 1.0 |
| Permissions-Policy | 1.0 |
| X-Frame-Options / frame-ancestors | 1.0 |
| Referrer-Policy | 0.5 |
| X-Content-Type-Options | 0.5 |

- **OK** → full weight applied  
- **Missing (graded)** → zero weight, included in denominator  
- **Missing (informational)** → shown in UI but carries no penalty  

Full scoring details:  
👉 *See the Scoring Model Reference (`scoring-models.md`)*

---

### Grades and Risk Levels  

HeaderCheck assigns a grade based on the final percentage:

| Score | Grade | Risk |
|--------|--------|--------|
| **≥ 85 percent** | A–B | Low |
| **< 85 percent** | C–D | Medium |
| **< 60 percent** | F | High |

**Critical headers:**  
Content-Security-Policy and Strict-Transport-Security.  
Missing one or both enforces a high-risk outcome.

---

### Informational Checks  

Some headers are surfaced for visibility but do **not** affect the score.  
These always appear in the UI as **Missing** with informational styling.

Their purpose is awareness, not penalty.

---

### Privacy  

HeaderCheck runs fully on-device:

- No telemetry  
- No logging  
- No external fetch calls  
- No use of remote services  

All evaluation occurs inside Chrome’s extension sandbox.  

See the [Unified Privacy Policy](https://yvonlabs.github.io/docs/privacy-policy) for platform-wide commitments.

---

### Security  

The extension adheres to the YvonLabs Security Policy:

- Deterministic local evaluation  
- Minimal permission footprint  
- Code review before packaging  
- Transparent scoring model and versioning  
- Static assets, no runtime external dependencies

---

### Release and Versioning  

- **Extension release:** `v0.1.0-dev`  
- **Scoring model:** `SCM-2025.1`  
- **Evaluation type:** deterministic weighted scoring  

All updates are tracked in [`CHANGELOG.md`](https://github.com/YvonLabs/headercheck/blob/main/CHANGELOG.md).

---

### Repository  

Installation instructions, source code, and contribution guidance:  
👉 https://github.com/YvonLabs/headercheck

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
