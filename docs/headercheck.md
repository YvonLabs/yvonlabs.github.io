# HeaderCheck  

**Type:** Chrome Extension  
**Maintained by:** YvonLabs  
**Current Model:** `SCM-2025.1`  
**Last Updated:** November 1, 2025  

---

### Overview  

HeaderCheck is a lightweight, privacy-respecting browser extension that inspects HTTP response headers for the active tab and evaluates the site’s security and privacy posture.  

It uses a deterministic Boolean scoring model (`SCM-2025.1`) to assign a score from **0–100**, based on header presence and relevance across five weighted categories.  
All processing occurs **locally within the browser** — no telemetry, remote calls, or data collection.

---

### Key Features  

- **Deterministic local scoring** — no API calls, no external dependencies.  
- **Instant analysis** — one click, one result.  
- **Weighted categories** based on real-world impact and privacy significance.  
- **Actionable findings** — quick explanations for missing or weak headers.  
- **EU-aligned defaults** emphasizing transport security and privacy.  

---

### Scoring Categories  

| Category | Weight | Description |
|-----------|--------|-------------|
| **Transport Security** | 25 | HSTS and HTTPS enforcement to prevent downgrade attacks |
| **Content Isolation** | 25 | CSP, X-Frame-Options, sandbox enforcement |
| **Privacy & Permissions** | 25 | Referrer-Policy, Permissions-Policy, Cross-Origin rules |
| **Cache & Lifetime** | 15 | Cache-Control, Expires, Pragma behavior |
| **Misc. Disclosure** | 10 | Server banners, legacy header exposure |

Each category contributes to a normalized total of 100 points.  
For the detailed header-level breakdown, see the [Scoring Model Reference](https://yvonlabs.github.io/docs/scoring-models).

---

### Score Bands  

| Range | Grade | Meaning |
|-------|-------|---------|
| **90–100** | ✅ Pass | Strong alignment with privacy and security best practices |
| **70–89** | ⚠️ Warning | Minor issues or missing best-practice headers |
| **<70** | ❌ Fail | Critical controls missing or misconfigured |

---

### Privacy  

HeaderCheck operates entirely on-device.  
It does **not** collect usage data, transmit logs, or contact any remote endpoints.  
All logic, evaluation, and rendering occur within Chrome’s extension sandbox.  

For global privacy commitments across all YvonLabs tools, see the  
[Unified Privacy Policy](https://yvonlabs.github.io/docs/privacy-policy).

---

### Security  

The extension follows YvonLabs’ [Security Policy](https://yvonlabs.github.io/docs/security), which defines:  
- **Local-only computation** (no remote dependencies)  
- **Least-privilege permissions**  
- **Transparent changelogs and deterministic model versions**  
- **Static review before Chrome Web Store submission**

---

### Release and Model Versioning  

- **Binary release:** `v0.1.0-dev`  
- **Model version:** `SCM-2025.1`  
- **Evaluation type:** deterministic Boolean scoring  

Model revisions are versioned independently in [`CHANGELOG.md`](https://github.com/YvonLabs/headercheck/blob/main/CHANGELOG.md).  
Historical versions remain available for audit or regression testing.

---

### Repository  

For installation instructions, code, or contribution guidelines, visit:  
👉 [HeaderCheck on GitHub](https://github.com/YvonLabs/headercheck)

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
