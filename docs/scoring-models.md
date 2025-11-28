
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
