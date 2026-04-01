# Security Policy

72Energy builds AI-powered tools for energy analysis, property intelligence, and intellectual property management. Our projects interact with LLM APIs, process sensitive patent data, and expose web endpoints — we take security seriously.

This policy covers all 72Energy repositories, including:

- **72Energy AHRN** — Adversarial Hierarchical Reasoning Network (Python SDK + FastAPI)
- **72Energy IP Master** — Patent and IP strategy management platform
- **PropertyIQ** — Property analysis frontend

If a repository does not have its own `SECURITY.md`, this policy applies.

## Supported Versions

We are a small team. Only the latest release on the `main` branch of each project receives security patches. We recommend always running the most recent version.

| Project | Supported Version |
|---------|-------------------|
| 72Energy AHRN | Latest on `main` |
| 72Energy IP Master | Latest on `main` |
| PropertyIQ | Latest on `main` |

## Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

We offer two channels for reporting. Use whichever you prefer:

### GitHub Security Advisories (preferred)

Navigate to the **Security** tab of the affected repository and select **Report a vulnerability**. This creates a private discussion space where we can collaborate on a fix before any public disclosure.

### Email

Send your report to **info@72energy.com**.

Use the subject line: `[SECURITY] <repo-name> — <brief description>`

### What to Include

- Affected project and version (or commit hash)
- Description of the vulnerability
- Steps to reproduce
- Impact assessment — what could an attacker achieve?
- Suggested fix (optional, but appreciated)

## Response Timelines

| Stage | Timeline |
|-------|----------|
| Acknowledgment of report | Within 48 hours |
| Initial assessment and severity rating | Within 5 business days |
| Status updates to reporter | Every 7 days until resolved |
| Fix for critical vulnerabilities | Target 14 days |
| Fix for high-severity vulnerabilities | Target 30 days |
| Fix for medium/low-severity vulnerabilities | Target 90 days |
| Coordinated public disclosure | After fix is released, or 90 days maximum |

We are a small team and genuinely appreciate your patience. If you have not received an acknowledgment within 48 hours, please follow up.

## API Keys and Secrets

All 72Energy projects use API keys for services such as Anthropic (Claude), Perplexity, OpenAlex, and USPTO. Our rules for handling them:

**For contributors:**

- Store all secrets in `.env` files. These are gitignored across all projects — never commit them.
- Use `.env.example` files with placeholder values only.
- Never hardcode keys, tokens, or credentials in source code.
- Never include secrets in issues, pull requests, or comments.

**If a key is accidentally committed:**

1. Consider the key compromised. Rotate it immediately through the provider's dashboard.
2. Remove it from git history using [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) or `git filter-repo`.
3. Notify the team at info@72energy.com if it affects shared infrastructure.

## AI and LLM Security

Our projects send user-provided content to LLM APIs (primarily Anthropic Claude). This introduces unique security considerations:

**Prompt injection:**
- Sanitize and validate all user inputs before including them in prompts.
- System prompts must not be exposed to end users.
- Cross-agent outputs in AHRN's multi-agent architecture (Systems Thinker, Domain Expert, Adversary, Pattern Detector) should be validated at each stage.

**Model output validation:**
- Never treat LLM output as authoritative for security-critical or legal decisions.
- Patent analysis results from IP Master must be reviewed by qualified humans before any legal filing.
- Sanitize model outputs before rendering in UIs or passing to downstream APIs.

**Data sensitivity:**
- Patent claims and IP strategy data are potentially trade secrets. Handle them accordingly.
- Do not log full prompt/response pairs in production. Use truncated or hashed identifiers.
- Understand the data retention policies of each third-party API provider before sending sensitive content.

## Web Endpoint Security

For AHRN's FastAPI endpoints and any future API surfaces:

- Require authentication on all endpoints. Do not expose APIs publicly without access controls.
- Restrict CORS to known origins only.
- Validate all request inputs with Pydantic models.
- Use HTTPS in production.
- Do not expose internal error details or stack traces to clients in production.
- Implement rate limiting to prevent abuse and detect anomalous usage patterns.

## Dependency Security

- Run `pip audit` (Python) and `npm audit` (Node.js) before submitting pull requests.
- We recommend enabling GitHub Dependabot alerts on all repositories.
- Pin dependency versions in production deployments.
- Review dependency changes carefully during code review.

## Safe Harbor

72Energy will not pursue legal action against anyone who:

- Reports vulnerabilities in good faith following this policy
- Avoids accessing data beyond what is necessary to demonstrate the issue
- Does not degrade service availability during testing
- Follows coordinated disclosure timelines

## Recognition

We credit reporters in release notes with their permission. While we do not currently operate a formal bug bounty program, significant findings will be publicly acknowledged.

## Contact

- **Security reports:** info@72energy.com
- **General inquiries:** info@72energy.com
- **GitHub:** [@alirazavi](https://github.com/alirazavi)
- **Website:**{www.72energy.com} (https://www.72energy.com/)
