# HeaderCheck – Scoring Model Reference  
**Model ID:** SCM-2025.1  
**Maintained by:** YvonLabs  
**Last Updated:** November 1 2025  

---

### Overview  
HeaderCheck applies a deterministic, weighted composite model to evaluate HTTP response headers.  
Each header contributes to a total score of 100, derived from its assigned weight.  
The model emphasizes **exploitability**, **privacy sensitivity**, and **scope of control**.  
All computation occurs locally within the user’s browser — no remote calls or telemetry.

---

### Weight Distribution  

| Category | Headers | Weight | Evaluation Basis |
|-----------|----------|--------|------------------|
| **Transport Security** | HSTS | 2.0 | HTTPS enforcement and downgrade protection |
| **Content Isolation** | CSP | 2.0 | XSS and resource injection defense |
| **Cross-Origin Isolation** | COOP, COEP, CORP | 1.0 each | Prevent data leaks and enforce context isolation |
| **Privacy & Permissions** | Permissions-Policy, Referrer-Policy | 1.0 + 0.5 | Restrict APIs and reduce referrer leakage |
| **Framing Controls** | X-Frame-Options or CSP `frame-ancestors` | 1.0 | Mitigate clickjacking |
| **MIME and Legacy Protections** | X-Content-Type-Options | 0.5 | Prevent MIME sniffing (must include `nosniff`) |

**Total weight:** 10.0 points (normalized to 100%)

---

### Header Evaluation Logic  

Each header is evaluated as **present** or **missing**, based on Boolean checks.  
Partial credit is not used except for the `nosniff` test in **X-Content-Type-Options**.

| State | Meaning | Score |
|-------|----------|-------|
| ✅ **Present** | Header exists and passes its validation | 1.0 |
| ❌ **Missing** | Header not found or fails validation | 0 |

The weighted score is calculated as:
Σ(weight × state) / Σ(weight) × 100

**Example pseudocode:**

```js
const percent = Math.round((sumOkWeights / sumWeights) * 100);

---

### Adjustments and Limits of the Current Model  

HeaderCheck’s model is intentionally deterministic and does **not** apply deductions or subjective penalties.  
No evaluation is made for directive strength (for example, CSP contents or HSTS `max-age`).

| Rule | Effect | Example |
|------|---------|----------|
| Weak or partial directives | Ignored (binary model) | CSP missing `default-src` not penalized |
| Deprecated headers | Neutral | No scoring impact |
| Conflicting directives | Lowest outcome applied | e.g., XFO missing but CSP `frame-ancestors` found |
| Mixed content | Not yet implemented | Future versions may deduct points |
| Server disclosure | Not scored | Reserved for future metadata checks |

---

### Example Evaluation (Actual Logic)  

| Header | State | Weight | Note |
|---------|:------:|-------:|------|
| Content-Security-Policy | ✅ | 2.0 | Present |
| Strict-Transport-Security | ❌ | 2.0 | Missing |
| Permissions-Policy | ✅ | 1.0 | Present |
| Cross-Origin-Opener-Policy | ✅ | 1.0 | Present |
| Cross-Origin-Resource-Policy | ✅ | 1.0 | Present |
| X-Frame-Options / `frame-ancestors` | ✅ | 1.0 | Present |
| Cross-Origin-Embedder-Policy | ❌ | 1.0 | Missing |
| Referrer-Policy | ✅ | 0.5 | Present |
| X-Content-Type-Options (`nosniff`) | ✅ | 0.5 | Present |

**Total weight:** 10.0  
**Score:** 7.0 / 10 × 100 = **70 %**  
**Risk Level:** Medium (score < 85 %)  
**Grade:** C  

---

### Risk and Grade Rules  

| Condition | Risk | Grade |
|------------|------|-------|
| Percent < 60 % | High | F |
| Percent < 85 % | Medium | D–C |
| Percent ≥ 85 % | Low | A–B |
| 2 + critical (CSP, HSTS) missing | Force High | ≤ D |
| 1 critical missing and < 85 % | Force High | ≤ D |

---

### Model Versioning  

Model identifiers follow the format `SCM-YYYY.#`.  
All revisions are recorded in [`CHANGELOG.md`](../CHANGELOG.md).  
Changes include header additions, weight shifts, or logic adjustments.  
Historical versions remain available for reproducibility in audits or regression tests.

---

### Model Transparency  

Scoring and header evaluation occur entirely within the browser’s extension context.  
No data is transmitted or stored externally.  
The model is open for verification, research alignment, and public audit.

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
