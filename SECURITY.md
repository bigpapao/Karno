# Security Policy

## Supported Versions

We release patches for security vulnerabilities. Which versions are eligible for receiving such patches depends on the CVSS v3.0 Rating:

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

Please report (suspected) security vulnerabilities to **[security@karno.com](mailto:security@karno.com)**. You will receive a response from us within 48 hours. If the issue is confirmed, we will release a patch as soon as possible depending on complexity but historically within a few days.

### What to Include

When reporting a vulnerability, please include:

1. **Description** of the vulnerability
2. **Steps to reproduce** the issue
3. **Potential impact** of the vulnerability
4. **Suggested fix** (if you have one)

### Security Measures

Karno implements several security measures:

- **Authentication**: JWT-based authentication with refresh tokens
- **Authorization**: Role-based access control (RBAC)
- **Input Validation**: Comprehensive input validation and sanitization
- **Rate Limiting**: API rate limiting to prevent abuse
- **HTTPS**: All data transmission encrypted with TLS
- **Security Headers**: Proper security headers implementation
- **SQL Injection Prevention**: Parameterized queries and ORM usage
- **XSS Protection**: Content Security Policy and input sanitization
- **CSRF Protection**: CSRF tokens for state-changing operations

### Security Best Practices for Contributors

1. **Never commit secrets** (API keys, passwords, tokens) to the repository
2. **Use environment variables** for sensitive configuration
3. **Validate and sanitize** all user inputs
4. **Follow the principle of least privilege** for database access
5. **Keep dependencies updated** and monitor for vulnerabilities
6. **Use HTTPS** for all external API calls
7. **Implement proper error handling** without exposing sensitive information

### Security Updates

Security updates will be announced:

1. In the project's release notes
2. Via GitHub Security Advisories
3. On our security mailing list (if you want to be added, email security@karno.com)

### Vulnerability Disclosure Timeline

1. **Day 0**: Vulnerability reported
2. **Day 1-2**: Initial response and vulnerability assessment
3. **Day 3-7**: Develop and test fix
4. **Day 8-14**: Release security patch
5. **Day 15**: Public disclosure (if applicable)

Thank you for helping keep Karno and its users safe!