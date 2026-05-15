---
date: "2026-05-15"
tags: 
link:
---

## Role prompting for specialized tasks

Role prompting involves instructing GitHub Copilot to act as a specific type of expert, which can significantly improve the quality and relevance of generated code for specialized domains. This approach helps accelerate development by getting more targeted solutions on the first try.

### Security expert role

When working on security-critical features, prompt Copilot to think like a security expert:

"Act as a cybersecurity expert. Create a password validation function that checks for common vulnerabilities and follows OWASP guidelines."

This approach typically generates code that includes:

- Input sanitization
- Protection against common attacks
- Industry standard validation patterns
- Security best practices