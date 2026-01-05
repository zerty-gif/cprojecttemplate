# Security

## Practices
- Validate all user inputs before use.
- Enforce RBAC with explicit policy checks.
- Encrypt sensitive data at rest and in transit.
- Avoid logging secrets; apply redaction.

## Components
- `InputValidator`: schema validation and sanitization.
- `AuthProvider`: authentication and session management.
- `AccessControl`: RBAC policy evaluation.
- `CryptoProvider`: encryption and key management.
