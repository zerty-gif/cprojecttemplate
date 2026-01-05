# Security and DevSecOps Overlay

## DevSecOps Principles
- **Shift-left security:** Integrate security checks early and continuously.
- **Automation-first:** Security controls executed in CI/CD.
- **Evidence-driven:** Results retained for audit and gate decisions.

## CI/CD Security Controls
- **Pre-commit/PR checks:** Linting, unit tests, SAST.
- **Build stage:** Dependency scanning and license checks.
- **Test stage:** DAST (where applicable) and security regression tests.
- **Deploy stage:** Signed artifacts, environment approvals, change tracking.

## Scanning Requirements
- **SAST:** Run on every pull request and main branch build.
- **DAST:** Run against test/staging environments on release candidates.
- **Dependency scanning:** Run on every build and weekly scheduled scan.
- **Secret scanning:** Continuous scanning for credentials.

## Secure Engineering Standards
- **Input validation:** Validate and sanitize all external inputs.
- **Authentication:** Enforce strong authentication (e.g., OIDC/OAuth2).
- **Authorization:** Role-based access control (RBAC) with least privilege.
- **Encryption:** Use TLS for data in transit; encrypt sensitive data at rest.
- **Secure coding:** Align with OWASP ASVS and internal standards.

## Evidence Retention
- Store scan results, approvals, and release artifacts in a controlled repository.
- Retention period: minimum 12 months (or per regulatory requirement).
- Evidence must link to build identifiers and release tags.

## Security Gate Criteria (High-Level)
- No critical/high vulnerabilities without approved mitigations.
- Secrets rotated if exposed during pipeline scans.
- Threat model updated for high-risk changes.
- Security sign-off documented in gate pack.

## Incident and Vulnerability Management
- **Triage:** Severity and exploitability assessed within 24 hours.
- **Remediation SLAs:**
  - Critical: 7 days
  - High: 14 days
  - Medium: 30 days
- **Post-incident review:** Document lessons learned and improvements.
