---
name: web-security-checklist
description: Security review for AI-built websites and web apps before they go live. Use whenever a project has a backend, database, login, forms, API keys, paid APIs (AI calls), file uploads, or gets deployed/hosted publicly — and when the user asks for a security check, audit or "is this safe to put online".
---

# Web Security Checklist

AI-generated web apps tend to ship the same handful of holes. Go through every section that applies to this project, check the actual code and config (not assumptions), and report each item as PASS / FAIL / N/A with file:line for failures. Fix FAILs before calling the project done, unless the user says otherwise.

Skip sections that clearly don't apply (a static page with no forms and no keys only needs sections 1, 6 and 9). Say which you skipped.

## 1. Secrets

- No API keys, database URLs, service-role keys or tokens in frontend code, HTML, or anything bundled for the browser. Search the build output too, not only the source.
- Keys that must exist client-side (e.g. a public anon key) are the restricted, public kind — never admin/service keys.
- Secrets live in environment variables or a server-side config that is not committed. `.env` is in `.gitignore`.
- No secrets in git history, logs, error messages or screenshots.

## 2. Authentication and authorization

- Every non-public route and API endpoint checks that the user is logged in — on the server, not only by hiding buttons in the UI.
- Every request that reads or changes a record checks that this user owns it or is allowed to (no "change the ID in the URL and see someone else's data").
- Passwords are hashed with a slow algorithm (bcrypt, scrypt, argon2) — never stored plain or with a fast hash. Prefer an existing auth provider over hand-rolled auth.
- Sessions/tokens expire, cookies are `HttpOnly`, `Secure`, `SameSite=Lax` or stricter.
- Logout and password change invalidate existing sessions; session IDs are regenerated after login.
- Password reset tokens are random, single-use and expire within an hour; login and reset errors don't reveal whether an account exists.
- State-changing requests from cookie-based sessions are protected against CSRF (SameSite plus a CSRF token or origin check).
- Admin accounts use two-factor authentication.

## 3. Database

- Database access rules are locked down: row-level security / security rules on, default deny, no "allow read, write: if true".
- Queries are parameterized or go through an ORM — no SQL built by string concatenation with user input.
- The database is not reachable from the internet unless it has to be.

## 4. Input and output

- All user input is validated on the server (type, length, allowed values) — client-side validation is only for UX.
- Output is escaped; no `innerHTML`/`dangerouslySetInnerHTML` with user content. If HTML must be rendered, it is sanitized with a maintained library.
- File uploads: type and size limits, stored outside the web root or in object storage, never executed.
- Features that fetch a user-given URL block internal addresses (localhost, 169.254.x, private ranges) to prevent SSRF.
- Incoming webhooks (payments, forms) verify the provider's signature before acting.

## 5. Abuse and cost

- Rate limiting on login, sign-up, password reset, contact forms and every endpoint that is expensive.
- Any endpoint that calls a paid API (AI models, email, SMS) is behind auth or strict rate limits, and the paid account has a hard spending cap set at the provider.
- Forms that send email have spam protection.

## 6. Transport and headers

- HTTPS everywhere, HTTP redirects to HTTPS.
- CORS allows only the origins that need it — no `*` together with credentials.
- Basic security headers set: `Content-Security-Policy` (at least a sane default), `X-Content-Type-Options: nosniff`, `Referrer-Policy`, `frame-ancestors`/`X-Frame-Options`.

## 7. Dependencies and errors

- No known-vulnerable dependencies (`npm audit` / equivalent), lockfile committed.
- Production errors don't leak stack traces, queries or internal paths to the browser.
- Debug routes, test accounts and admin panels are removed or protected.

## 8. AI features (apps that call Claude or another model)

- The model API key and system prompt stay on the server; the browser only talks to your own endpoint.
- User text sent to the model is treated as untrusted: it cannot change the system prompt, unlock tools or read other users' data (prompt injection). Tool calls the model makes are checked against the logged-in user's permissions.
- Model output is escaped like any other user content before rendering; never executed or used as raw SQL/HTML.
- Per-user limits on tokens or requests, plus the provider spending cap from section 5.

## 9. Before going live

- Run through the app logged out, as a second user, and with tampered requests (changed IDs, missing fields, huge inputs).
- Confirm backups exist for anything with user data.
- Write the result as a short table: section, status, what was fixed, what is left for the user to decide.

## Ready prompts

Paste one of these into Claude Code when you want a single area checked instead of the full run:

- "Check this repo for secrets: search source, build output and git history for API keys, tokens and database URLs. List each with file:line and move them to env variables."
- "Audit every API route: does it check login on the server and that the user owns the record? Show the routes that don't."
- "Find every database query built from user input without parameters, and every `innerHTML`/`dangerouslySetInnerHTML` with user content. Fix them."
- "Review CORS, cookies and security headers against web-security-checklist section 6 and set them."
- "List all endpoints that cost money or send email and add rate limits."
- "Check the AI features against web-security-checklist section 8, including a prompt-injection test with a hostile user message."
- "Run the full web-security-checklist pre-launch pass as a logged-out user and as a second user, then give me the table."

---
Written in own words from public "vibe coding security checklist" material; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
