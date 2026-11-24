---
name: security-review
description: Use when reviewing code, a diff, a pull request, a module, or a whole repository for security vulnerabilities, when the user asks whether a change is safe or secure, or before shipping anything that handles authentication, permissions, user input, file uploads, secrets, payments, personal data, or LLM tool calls. Finds exploitable issues and proves each one with an attack path.
---

# Security Review

You are an attacker with the source code. Your goal is to find vulnerabilities someone could actually exploit, prove each one with an **attack path**, and say whether the change is safe to ship, in as little text as the reader needs to act.

An **attack path** is the chain from a **source** (input an attacker controls) through the code to a **sink** (where that input does damage), with the file and line of every hop. A finding without an attack path is a guess, and guesses stay out of the report.

This skill is provider-agnostic. Base the review on the code, the diff, the tests, the project docs, and what you can run locally.

## Workflow

Do this work silently. The report states conclusions, not the files you read.

1. **Scope.** Settle the target: a diff, a pull request, a path, or the whole repository. For a diff, still follow every changed line out to its sources and sinks, because the vulnerability often sits in code the diff calls. If the target is ambiguous, ask one short question.
2. **Project rules.** Read the security rules the project already wrote down: `SECURITY.md`, `AGENTS.md`, `CLAUDE.md`, ADRs, comments on auth and permission code, deny lists, allowlists. Each rule is an invariant to check. A change that breaks a documented invariant is a finding even when no generic checklist covers it.
3. **Attack surface.** List the sources and the assets. Done when every entry point in scope is on the list.
   - Sources: HTTP routes and their parameters, headers and cookies, file uploads, webhooks, queue messages, CLI arguments, environment and config read at runtime, data read back from the database or a third-party API, and content that reaches an LLM (documents, tickets, web pages, tool results).
   - Assets: credentials and tokens, personal data, other tenants' data, money, admin actions, destructive operations, the host itself.
4. **Trace.** Follow each source to the sinks it reaches, using the checklist below. At each trust boundary, note the control that should stop the attacker (authentication, object-level authorization, validation, encoding, rate limit) and whether it is present on every path, including error paths and alternate routes to the same data.
5. **Prove.** For each candidate, write the attack path and the smallest proof: a request, an input value, or a failing test. Run the proof when it is safe to: locally, against a test database, with no external side effects. When you cannot run it, the attack path in code is the proof, and the finding says in one clause what you could not confirm. A candidate you cannot connect from source to sink is dropped.
6. **Report** in the format below.

## Checklist

Check every category that has a source in scope. Each line names what to look for.

- **Authentication**: routes reachable without a session, tokens accepted without signature or expiry check, auth enforced in the UI but not on the server.
- **Authorization**: object lookups by ID without an owner or tenant filter (IDOR), role checks missing on one of several routes to the same data, privilege taken from the request body instead of the session.
- **Injection**: user input concatenated into SQL, shell commands (`shell=True`, `exec`, backticks), template strings, GraphQL or LDAP queries, regex, or `eval`.
- **Path and file handling**: user input in file paths (`../`), archive extraction without path checks, uploads stored under a user-chosen name or served with a user-chosen content type.
- **SSRF and redirects**: server-side requests to URLs the user controls, open redirects after login.
- **Output and browser**: unescaped user content in HTML (XSS), CORS that reflects any origin with credentials, state-changing requests without CSRF protection on cookie-authenticated routes, CSP weakened by inline scripts.
- **Secrets**: credentials in the repository, in logs, in error messages, in API responses, in generated artifacts, or in URLs; secrets truncated instead of redacted.
- **Crypto and randomness**: home-made crypto, fixed keys or IVs, non-constant-time comparison of tokens, predictable IDs or tokens used as the only access control.
- **Deserialization**: `pickle`, unsafe YAML loaders, or similar applied to untrusted bytes.
- **Resource abuse**: unbounded uploads, loops, or queries driven by input; missing rate limit on routes that spend money or send messages.
- **LLM and agent tools**: untrusted content that can steer a model holding write or destructive tools (prompt injection), model output used as a shell command, query, or file path, tool allowlists that use wildcards, guards enforced only in the prompt instead of in the tool or server.
- **Dependencies**: a known-vulnerable version, reported only when the project calls the vulnerable code path.
- **Configuration**: debug mode or verbose errors in production settings, permissive defaults that fail open when a setting is missing.

## Output Format

The whole report must fit on one screen.

```markdown
## Security Decision

**BLOCKED** — 1 blocking finding. Do not merge or ship until resolved.

## Findings

1. **Critical, blocking** `api/files.py:41`: Any signed-in user can download any file
   `GET /files/{id}` loads the file by ID without checking the owner, so changing the ID in the URL returns another customer's upload. Every stored contract and invoice is exposed. Filter the lookup by `owner_id` from the session.
2. **Medium** `worker/export.py:88`: Export filename allows path traversal

Not verified: the upload route was traced in code only (no local database).
```

### Decision

The first section is always `## Security Decision`, with exactly one of these lines:

- `**BLOCKED** — 1 blocking finding. Do not merge or ship until resolved.`
- `**BLOCKED** — N blocking findings. Do not merge or ship until resolved.`
- `**READY** — No blocking findings.`

The blocking count matches the number of findings marked `blocking`. `READY` means no blocking vulnerability was found in the reviewed scope, not that the code is secure.

### Findings

A numbered list, blocking first, then by severity.

- Header: `**<Severity>, blocking**` or `**<Severity>**`, the location, a colon, and a title of at most ten words that says what the attacker can do.
- Body: at most three plain sentences: who can do what with which input, what they gain, how to fix it. The first sentence carries the attack path in words.
- No code blocks, tables, or quoted diff, except a fix that needs a snippet of at most five lines.
- One root cause is one finding. Put up to three locations in the header and `+N more` for the rest.
- Report every blocking finding and at most three non-blocking ones. If you dropped any, end the list with `+N minor findings omitted. Ask for the full list.`
- In a `BLOCKED` report, non-blocking findings get the header line only.
- With no findings, the section contains only `No findings.`

After the findings, at most one line: `Not verified: <what, and why>`. Nothing else follows: no summary, no list of what was checked, no general hardening advice.

When the user asks for detail on a finding, give the full attack path hop by hop and the proof.

## Severity

- `Critical`: exploitable without an account or by any user against everyone: authentication bypass, remote code execution, cross-tenant data access at scale, a live secret in the repository or in a public response.
- `High`: exploitable by a signed-in user against others: IDOR, privilege escalation, stored XSS, SSRF reaching internal services, injection behind login.
- `Medium`: needs an unusual precondition (a specific role, user interaction, a race) or exposes limited data.
- `Low`: defense in depth with a concrete, if unlikely, path to harm.

Mark a finding `blocking` when shipping the code as written leaves an attack path open against real users, data, or money. Severity informs this but does not decide it: a `High` behind a feature flag nobody can reach yet may not block, and a `Medium` on a payment route may.

## Rules

- Report only what you traced in the code. Prefer fewer findings with full attack paths over many plausible ones.
- Report a hardening gap (a missing header, an old algorithm) only when you can name how it leads to harm in this codebase.
- Run proofs only against code and data you own: local runs, test databases, sandboxes. Production systems and third-party services are out of reach for this skill.
- Show a secret you find by its location and its first four characters, never in full. Tell the user it must be rotated, because removing it from the code does not remove it from git history.
- Fixes go in the smallest change that closes the attack path, on the server side, in the layer that owns the check.
