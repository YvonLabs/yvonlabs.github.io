# HeaderCheck – Scoring Model Reference  
**Model ID:** SCM-2025.1  
**Maintained by:** YvonLabs  
**Publication:** Initial Release

---

## Overview  
HeaderCheck evaluates HTTP response headers using a deterministic, weighted scoring model.  
Each header contributes a fixed portion of a one-hundred-point composite score, based on its relevance to modern security and privacy best practices.

HeaderCheck recognizes three evaluation states:

1. **OK** – header present and valid  
2. **Missing (graded)** – header absent and reduces the score  
3. **Missing (informational)** – header absent but carries no penalty  

All computation happens entirely within the browser. No requests are sent anywhere.

---

## Weight Model  

The scoring system focuses on areas that provide the most meaningful protection: transport security, content isolation, cross-origin behavior, privacy controls, and clickjacking resistance.

| Category | Headers | Weight | Purpose |
|----------|----------|--------|---------|
| Transport Security | Strict-Transport-Security | 2.0 | Prevents protocol downgrade and enforces HTTPS |
| Content Isolation | Content-Security-Policy | 2.0 | Primary defense against XSS and resource injection |
| Cross-Origin Isolation | COOP, COEP, CORP | 1.0 each | Context isolation and prevention of cross-origin data leaks |
| Privacy Controls | Permissions-Policy, Referrer-Policy | 1.0 and 0.5 | API restriction and referrer minimization |
| Framing Protections | X-Frame-Options or frame-ancestors | 1.0 | Mitigates clickjacking |
| MIME Protection | X-Content-Type-Options | 0.5 | Prevents MIME sniffing when set to nosniff |

**Total weight:** 10.0 points, normalized to one hundred.

---

## Header Evaluation Logic  

HeaderCheck determines the state of each header using consistent, deterministic rules.

---

### 1. OK state  
A header is considered OK when present and passing validation.

- UI classification: **OK**  
- Styling: green  
- Score impact: full weight is applied

---

### 2. Graded missing headers reduce the score  

Graded headers are required security controls that participate in the scoring model.  
When a graded header is missing or invalid:

- UI classification: **Missing**  
- Styling:  
  - **missing** for severe issues  
  - **weak** for lower-severity cases  
- Score impact:  
  - Contributes zero to the OK-weight total  
  - Weight remains included in the total graded weight  
  - Final percentage decreases  
- Behavior:  
  - All graded headers affect scoring  
  - Only headers explicitly marked `graded:false` are excluded

---

### 3. Informational missing headers do not reduce the score  

Some checks are helpful to surface but not appropriate to penalize.  
When an informational header is absent:

- UI classification: **Missing**  
- Styling: informational weak state  
- Score impact: none  
- Weight: not included in either the numerator or denominator  
- Purpose: visibility without penalty

Examples include optional best-practice hints and advisory controls.

---

## Scoring Formula  

Only graded headers participate in the mathematical model.
score = round( (sum of OK graded weights / sum of all graded weights) × 100 )

Informational checks are excluded.

---

## Example Evaluation  

| Header | State | Graded | Weight | Contribution |
|--------|--------|--------|---------|-------------|
| Content-Security-Policy | OK | Yes | 2.0 | 2.0 |
| Strict-Transport-Security | Missing | Yes | 2.0 | 0 |
| COOP | OK | Yes | 1.0 | 1.0 |
| Permissions-Policy | Missing | No | 1.0 | Ignored |
| COEP | Missing | Yes | 1.0 | 0 |
| Referrer-Policy | OK | Yes | 0.5 | 0.5 |
| X-Content-Type-Options | OK | Yes | 0.5 | 0.5 |

**Total graded weight:** 7.0  
**Total OK graded weight:** 4.0  
**Final score:** 57 percent  
**Grade:** D  
**Risk:** Medium to High  

Critical missing headers in this example: HSTS and COEP.

---

## Grade and Risk Classification  

| Score | Risk | Grade |
|--------|--------|--------|
| Below 60 percent | High | F |
| Below 85 percent | Medium | C to D |
| At or above 85 percent | Low | A to B |
| Two or more critical headers missing | High | Forced D or lower |
| One critical missing and score below 85 percent | High | Forced D |

**Critical headers:**  
Content-Security-Policy and Strict-Transport-Security.

---

## Informational Checks  

HeaderCheck surfaces certain optional or advisory headers to improve transparency.  
These checks:

- are displayed in the UI  
- always appear as Missing  
- do not reduce the score  
- help developers understand potential improvements that do not fall under mandatory security protections

Examples include optional feature policies or future best-practice recommendations.

---

## Model Versioning  

Model identifiers follow the pattern:

---

### Model Versioning  

Model identifiers follow the format `SCM-YYYY.#`.  
All revisions are recorded in [`CHANGELOG.md`](../CHANGELOG.md).  
Future revisions may expand categories, adjust weights, or add new informational checks while preserving backward reproducibility.

---

### Model Transparency  

All evaluation logic runs locally in the extension.  
HeaderCheck does not transmit data, store results externally, or create any form of telemetry.  
The scoring model is fully deterministic and auditable.

---

<p align="center">
  <sub>Minimal • Fast • Focused © YvonLabs</sub>
</p>
