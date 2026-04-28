# Security Policy

## Supported Versions

| Version | Supported |
|---|---|
| 0.1.x | Yes |

## Reporting a Vulnerability

Please report security issues privately through GitHub Security Advisories or direct maintainer contact.

Include:
- Affected endpoint or component
- Reproduction steps
- Impact assessment
- Suggested mitigation (if available)

## Security Baseline

- Input schema validation at API boundary
- Payload size restrictions to reduce abuse risk
- Host header validation for trusted domains
- Optional HSTS for strict transport security in production
- No hard-coded secrets in source
