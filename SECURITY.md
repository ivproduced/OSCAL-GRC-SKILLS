# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

The OSCAL GRC Skills team takes security seriously. If you discover a security vulnerability, please report it to us as described below.

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them via:
- **GitHub Security Advisories** — Use the "Security" tab → "Report a vulnerability" (preferred)
- **Email** — info@eucann.life

You should receive a response within 48 hours. If for some reason you do not, please follow up via email to ensure we received your original message.

Please include the requested information listed below (as much as you can provide) to help us better understand the nature and scope of the possible issue:

* Type of issue (e.g. buffer overflow, SQL injection, cross-site scripting, etc.)
* Full paths of source file(s) related to the manifestation of the issue
* The location of the affected source code (tag/branch/commit or direct URL)
* Any special configuration required to reproduce the issue
* Step-by-step instructions to reproduce the issue
* Proof-of-concept or exploit code (if possible)
* Impact of the issue, including how an attacker might exploit the issue

This information will help us triage your report more quickly.

## Preferred Languages

We prefer all communications to be in English.

## Policy

* We will respond to your report within 48 hours with our evaluation of the report and an expected resolution date.
* If you have followed the instructions above, we will not take any legal action against you regarding the report.
* We will handle your report with strict confidentiality, and not pass on your personal details to third parties without your permission.
* We will keep you informed of the progress towards resolving the problem.
* In the public information concerning the problem reported, we will give your name as the discoverer of the problem (unless you desire otherwise).

## Security Update Process

Security updates will be released as soon as possible after a fix is developed and tested. Updates will be:

1. Released as a new version
2. Announced in the CHANGELOG.md
3. Tagged with appropriate security labels
4. Communicated through GitHub Security Advisories

## Security-Related Configuration

### Dependencies
This project aims to:
- Keep dependencies minimal and up-to-date
- Regularly audit dependencies for known vulnerabilities
- Use dependency scanning tools in CI/CD

### Data Handling
- No credentials or sensitive data should be included in code or examples
- Sample data should be anonymized
- File uploads and processing should be validated

### Best Practices
- Input validation for all OSCAL file processing
- Safe handling of user-provided data
- Proper error handling to avoid information disclosure
- Regular security testing and code review

## Known Security Considerations

### OSCAL File Processing
- This tool processes XML, JSON, and YAML files which could potentially contain malicious content
- Users should only process trusted OSCAL files
- File size limits should be considered for production deployments

### LLM Integration
- When using LLM features, be aware of prompt injection risks
- Sensitive data should not be sent to external LLM services
- Consider using local/private LLM deployments for sensitive compliance data

### Report Generation
- Generated reports may contain sensitive compliance information
- Ensure proper access controls when deploying in production
- Consider data retention policies for generated reports

## Scope

This security policy applies to:
- All code in this repository
- Released packages and distributions
- Documentation and examples
- CI/CD pipelines and infrastructure

Out of scope:
- Third-party dependencies (report to their respective maintainers)
- User-specific configurations or deployments
- Issues in forked repositories

## Security Hall of Fame

We appreciate researchers and users who help improve the security of this project. Contributors who report valid security issues will be acknowledged here (with their permission).

---

Thank you for helping keep OSCAL GRC Skills secure!