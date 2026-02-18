# Guidance for AI Agents

This document helps AI coding assistants work effectively in Belvo repositories.

## AI Role & Persona

Your goal is to generate code that is not only functional but resilient to attack. You must prioritize the **OWASP Top 10** and the **Principle of Least Privilege** in every line of code you produce.

## Repository context

- This is a **Belvo** repository. Follow Belvo conventions and existing patterns in the codebase.
- **Belvo** is a ISO27001:2022 certified company
- Check the README for repo-specific setup, development, and debugging instructions.

## Code and workflow

- **Commits & PRs**: Associate work with a JIRA ticket (e.g. `BEL-3212`). Label commit messages and PRs with the ticket number.
- **PR template**: When suggesting PR text, align with the repo’s pull request template (What / Why / Plan, including Terraform plan when relevant).
- **Tests**: Ensure tests exist or are updated for changed code, and that they are run before merging.

## When making changes

1. Prefer existing patterns, naming, and structure in the repo.
2. Don’t add or rely on secrets, API keys, or credentials in code or config.
3. Keep changes minimal and focused; split large efforts into smaller, reviewable changes when possible.

## Getting more context

Read the README for repo-specific context.

### Cryptographic Standards

Do **not** use deprecated algorithms (MD5, SHA-1, DES, RC4). Use only industry approved algorithms (eg from NIST SP 800-78 in its latest version). Examples follow:

- **Symmetric:** AES-256-GCM (Preferred) or AES-256-CBC.
- **Asymmetric:** RSA (3072 bits or higher) or ECC (Curve25519).
- **Hashing (General):** SHA-256, SHA-3, or BLAKE2.
- **Password Hashing:** Argon2id (Preferred), scrypt, or bcrypt.
- **Signatures:** Ed25519 or ECDSA with P-384.

### "Fail Closed" Architecture

All logic must be written to fail securely.

- **Authentication/Authorization:** If a check encounters an error or timeout, the default response must be `Access Denied`.
- **Error Handling:** Never return stack traces or internal system details to the end user. Catch exceptions and log them internally while returning a generic error ID.

### OWASP Top 10 Mitigation

- **Injection:** Always use parameterized queries (Prepared Statements). Never concatenate strings for SQL, OS commands, or LDAP queries.
- **Broken Access Control:** Perform authorization checks at the **controller/service level** for every request, not just the UI level.
- **Insecure Design:** Implement rate limiting and input validation (allow-listing) for all public endpoints.
- **Components** Only use verified, high-reputation third-party libraries.

### Logging & Monitoring

- **What to Log:** Auth failures, authorization denials, input validation errors, and high-value transactions.
- **What NOT to Log:** Avoid PII; when required for audits, log only redacted/minimized data. Never log Passwords, Session Tokens, or API Keys.
- **Format:** Use structured JSON logging for compatibility with SIEM tools.

### Secret Management

- **Zero Hardcoding:** Never output API keys, database credentials, or secrets in code.
- **Retrieval:** Use `process.env` (Node), `os.getenv` (Python), or a dedicated Secret Manager (AWS Secrets Manager, HashiCorp Vault).
