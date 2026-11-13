# Security: Good Morning Breach

This file owns the secure-coding rules. `REQUIREMENTS.md` owns WHAT the system does, `DESIGN.md` owns how it looks and behaves, and `ARCHITECTURE.md` owns components, stack, and trust boundaries (TB-1 to TB-5). This file contains no threat model or risk scoring.

## Secure-Coding Inputs

**Documents read (2026-11-13):** `REQUIREMENTS.md`, `DESIGN.md`, `ARCHITECTURE.md`. No earlier `SECURITY.md` existed, so there are no inherited rule IDs.

**Security notes from the owner:** "this is person project" (personal project). This confirms NFR-1.1 and adds no new scope.

**Interview:** the owner told the author to answer all open questions. Decisions made on that instruction are marked *(delegated decision)*.

**Confirmed components (from ARCHITECTURE.md, Stack):**
- Go 1.27.x (`net/http`, `crypto/*`, `html/template`, `log/slog`, `net/smtp`); Gin v1.12.x
- PostgreSQL 18.x via `github.com/jackc/pgx/v5` (PROPOSED); `golang.org/x/crypto/argon2` (PROPOSED); `github.com/pquerna/otp` (PROPOSED); `github.com/mmcdole/gofeed` (PROPOSED)
- React + React DOM 19.3.x; TypeScript 7.0.x; Vite 8.3.x (PROPOSED); Node.js 26.x LTS (build machine only, PROPOSED); npm; Vitest (PROPOSED)
- Outbound: SMTP (owner's mail account, provider UNKNOWN), Twilio Programmable Messaging REST API 2010-04-01, Slack incoming webhooks, HIBP Pwned Passwords range API v3, collection sources (FR-1.14), MITRE ATT&CK STIX bundle (data file)
- Deployment: one machine, server on localhost only with a local TLS certificate, one Go process, local PostgreSQL (AQ-1, AQ-2)

Rules for PROPOSED components apply only while those components stay in the stack.

**Applicability decisions:**
- *Request and resource limits:* applicable (TB-1 bodies, TB-2 feed sizes, server timeouts).
- *Event-loop blocking:* not applicable as an event loop. Go has no single event loop and Node does not run in production. The Go equivalent applies: bounded goroutines and context deadlines on all I/O (SC-030).
- *Input validation, output encoding, authentication, authorization, sessions, CSRF, errors, logging, dependencies:* applicable.
- *Runtime permissions:* applicable to the OS user, the PostgreSQL role, and secrets on disk (TB-4).
- *Prototype pollution:* applies only to the React client, which handles untrusted keys such as category and source names. Go server: not applicable, because Go structs and maps have no prototype chain. Node at runtime: not applicable.
- *Unsafe code execution:* applicable. This covers `dangerouslySetInnerHTML`, `eval`, `text/template` for HTML, Go `unsafe`, `os/exec`, and `reflect`-driven deserialization.
- *File uploads, OAuth/OIDC, JWT/self-contained tokens, WebRTC, public APIs, CORS for third parties:* not applicable. No requirement includes them, and the design uses server-side sessions.
- *Inbound webhooks (Twilio or Slack signatures):* not applicable. ARCHITECTURE.md says there are no inbound connections from outside the machine.
- *LLM or AI-specific controls:* not applicable. The Analyzer uses local rules only (AQ-3).

**Gaps and conflicts:**
- FR-6.6 sets a 12-character minimum. NIST SP 800-63B-4 allows 8 when the password is used with MFA and requires 15 when it is the only factor. Login always needs TOTP (FR-6.5), so 12 is stricter than the source. No conflict.
- These gaps were resolved by delegated decision (former OD-001 to OD-008):
  - absolute session timeout (FR-6.10 sets only an idle timeout): SC-061
  - secrets at rest: SC-071
  - local TLS certificate and HSTS: SC-002, SC-007
  - phone verification code limits (FR-4.15): SC-056
  - lost TOTP device: SC-057
  - rate limits on messages the system sends: SC-058
  - application log retention: SC-083
  - version pinning policy for PROPOSED packages: SC-091
- The OS of the owner's machine is still UNKNOWN. SC-071 is written so that it does not depend on the OS.
- Could not be verified against official docs, so no rule depends on it:
  - whether React 19 blocks `javascript:` URLs (SC-041 enforces the scheme itself)
  - the TypeScript 7 `strict` default (SC-044 sets it explicitly)
  - Gin's default trusted-proxy behaviour (SC-006 sets it explicitly)
  - Twilio STOP handling

## Sources

All retrieved 2026-11-13.

- **S-01 Go release history**: https://go.dev/doc/devel/release, support policy and go1.27.4 entry. Supports: Go.
- **S-02 net/http (go1.27.4)**: https://pkg.go.dev/net/http, sections `Server`, `MaxBytesReader`, and `CrossOriginProtection` (added go1.25). Supports: Go server.
- **S-03 net/smtp**: https://pkg.go.dev/net/smtp, package overview ("frozen"), `PlainAuth`, `SendMail` (opportunistic STARTTLS). Supports: email channel.
- **S-04 crypto/rand (go1.27.4)**: https://pkg.go.dev/crypto/rand, `Text` (go1.24+) and `Read`. Supports: tokens and sessions.
- **S-05 encoding/xml**: https://pkg.go.dev/encoding/xml, `Decoder.Strict` and `Entity`. Supports: Collector (via gofeed).
- **S-06 Gin**: https://pkg.go.dev/github.com/gin-gonic/gin (`SetTrustedProxies`, `SetMode`, `BindJSON`) and https://gin-gonic.com/en/docs/deployment/. v1.12.x. Supports: HTTP API.
- **S-07 pgx v5**: https://pkg.go.dev/github.com/jackc/pgx/v5, placeholders, `Identifier.Sanitize`, simple-protocol warning. Supports: data access.
- **S-08 pquerna/otp totp**: https://pkg.go.dev/github.com/pquerna/otp/totp and https://github.com/pquerna/otp/blob/master/totp/totp.go, `Validate`, `ValidateCustom`, `ValidateOpts`. v1.5.0 page. Supports: Identity.
- **S-09 PostgreSQL 18 release notes**: https://www.postgresql.org/docs/18/release-18.html, MD5 deprecation and libpq `sslkeylogfile`. Supports: PostgreSQL.
- **S-10 OWASP Password Storage Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html#argon2id. Supports: Identity.
- **S-11 NIST SP 800-63B Rev. 4**: https://pages.nist.gov/800-63-4/sp800-63b.html, §3.1.1.2 (passwords) and §3.1.4.2 / §3.1.5.2 (OTP replay). Page dated 2025-08-26. Supports: Identity.
- **S-12 OWASP Session Management Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html, sections Cookies, Cookie name prefixes, Renew the session ID after any privilege level change, Idle timeout, and Absolute timeout. Supports: HTTP API, Identity.
- **S-13 OWASP CSRF Prevention Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html, sections "Disallowing Simple Requests" and "Fetch Metadata Headers". Supports: HTTP API, React client.
- **S-14 OWASP Content Security Policy Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html, strict and basic policies, `frame-ancestors`. Supports: HTTP API, React client.
- **S-15 OWASP HTTP Headers Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html, HSTS, X-Content-Type-Options, Referrer-Policy, COOP, Cache-Control, Server, and X-Powered-By. Supports: HTTP API.
- **S-16 OWASP SSRF Prevention Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html, case 2 (any external destination), DNS rebinding/TOCTOU, redirects, and schemes. Supports: Collector, channel adapters.
- **S-17 OWASP Prototype Pollution Prevention Cheat Sheet**: https://cheatsheetseries.owasp.org/cheatsheets/Prototype_Pollution_Prevention_Cheat_Sheet.html, Map/Set and `Object.create(null)`. Supports: React client.
- **S-18 OWASP ASVS 5.0**: https://github.com/OWASP/ASVS/tree/master/5.0/en, chapters V1 to V16. Used for area coverage only. Supports: all.
- **S-19 React DOM common components**: https://react.dev/reference/react-dom/components/common, `dangerouslySetInnerHTML`. React 19.x. Supports: React client.
- **S-20 Vite shared options**: https://vite.dev/config/shared-options#envprefix. Supports: Vite build.
- **S-21 Vite build options**: https://vite.dev/config/build-options#build-sourcemap (default `false`). Supports: Vite build.
- **S-22 Vite server options**: https://vite.dev/config/server-options, `server.host`, `server.fs.strict`, `server.fs.deny`, `allowedHosts`, `server.cors`. Supports: Vite dev server.
- **S-23 npm ci**: https://docs.npmjs.com/cli/v11/commands/npm-ci, lockfile requirement and `ignore-scripts`. Supports: client build.
- **S-24 npm audit**: https://docs.npmjs.com/cli/v11/commands/npm-audit, "Audit Signatures". Supports: client build.
- **S-25 Node.js previous releases**: https://nodejs.org/en/about/previous-releases, v26 LTS status. Supports: build machine.
- **S-26 HIBP API v3**: https://haveibeenpwned.com/API/v3, "Searching by range" (`api.pwnedpasswords.com/range/{prefix}`, `Add-Padding`). Supports: Identity.
- **S-27 Slack incoming webhooks**: https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks, URL format and "contains a secret". Supports: Slack adapter.
- **S-28 Slack formatting**: https://docs.slack.dev/messaging/formatting-message-text, escaping `&`, `<`, and `>`. Supports: Slack adapter.
- **S-29 Twilio API keys**: https://www.twilio.com/docs/iam/api-keys, key types (Main, Standard, Restricted) and per-subsystem keys. Supports: SMS adapter.

## Secure-Coding Rules

### Transport, server limits, and headers

**SC-001 — HTTPS only on localhost**
- **Status:** ACTIVE
- **Rule:** The server MUST listen only on a loopback address with TLS, and MUST NOT serve plain HTTP.
- **Enforcement:** `http.Server` setup in the HTTP API.
- **Evidence:** NFR-3.1; ARCHITECTURE.md AQ-1; S-15 (HTTPS). Loopback-only binding is a project decision (AQ-1).
- **Verification:** A connection to the machine's LAN IP is refused. An `http://` request gets no response. `https://localhost` succeeds.

**SC-002 — TLS configuration**
- **Status:** ACTIVE
- **Rule:**
  - The server and every outbound client MUST set `tls.Config.MinVersion` to at least `tls.VersionTLS12` explicitly, and MUST NOT set `InsecureSkipVerify`.
  - The localhost certificate MUST be issued by a local certificate authority that the owner's OS trust store trusts. It MUST cover only `localhost`, `127.0.0.1`, and `::1`.
  - The CA private key and the server key MUST be `0600` files outside the repository. Users MUST NOT be asked to click through certificate warnings. *(delegated decision)*
- **Enforcement:** The shared TLS config used by the HTTP API and all outbound clients; install steps.
- **Evidence:** NFR-3.1; S-15. Setting the version explicitly and the certificate approach are project decisions.
- **Verification:**
  - A TLS 1.1 client handshake fails.
  - A code search finds no `InsecureSkipVerify: true`.
  - `https://localhost` loads without a browser warning.
  - The certificate's SAN list has no other names.

**SC-003 — Server timeouts**
- **Status:** ACTIVE
- **Rule:** The `http.Server` MUST set non-zero `ReadHeaderTimeout`, `ReadTimeout`, `WriteTimeout`, and `IdleTimeout`.
- **Enforcement:** HTTP API server construction.
- **Evidence:** S-02, `Server` (zero means no timeout).
- **Verification:** A unit test asserts all four are greater than 0. A client that sends headers slowly is disconnected.

**SC-004 — Request size limits**
- **Status:** ACTIVE
- **Rule:** Every request body MUST be wrapped with `http.MaxBytesReader`, with a limit of 64 KiB (project decision), before it is parsed. Requests over the limit MUST get 413.
- **Enforcement:** Gin middleware on all routes.
- **Evidence:** S-02, `MaxBytesReader`. The 64 KiB value is a project decision: no form in DESIGN.md needs more.
- **Verification:** A 65 KiB JSON POST returns 413, and the handler never runs.

**SC-005 — Release mode**
- **Status:** ACTIVE
- **Rule:** The production binary MUST run Gin in `gin.ReleaseMode`.
- **Enforcement:** `main` at startup.
- **Evidence:** S-06, `SetMode`.
- **Verification:** At startup, `gin.Mode()` equals `release`. Debug route logs are absent.

**SC-006 — No trusted proxies**
- **Status:** ACTIVE
- **Rule:** The server MUST call `SetTrustedProxies(nil)`, so `X-Forwarded-For` and `X-Real-IP` are never used for the client IP.
- **Enforcement:** Gin engine setup.
- **Evidence:** S-06, `SetTrustedProxies`. There is no proxy in the architecture (AQ-1).
- **Verification:** A request with `X-Forwarded-For: 1.2.3.4` logs the loopback address, not `1.2.3.4`.

**SC-007 — Security headers**
- **Status:** ACTIVE
- **Rule:** Every response MUST carry these headers:
  - `X-Content-Type-Options: nosniff`
  - `Referrer-Policy: strict-origin-when-cross-origin`
  - `Cross-Origin-Opener-Policy: same-origin`
  - `Cache-Control: no-store` on API responses
  
  Responses MUST NOT carry `X-Powered-By` or a version in `Server`. Responses MUST NOT send `Strict-Transport-Security`, because HSTS on `localhost` would apply to every localhost port in the browser. SC-001 already refuses plain HTTP. *(delegated decision)*
- **Enforcement:** Gin middleware.
- **Evidence:** S-15, sections for each header and the HSTS caution. `no-store` on all API responses is a project decision, because every API response is per-user. Omitting HSTS is a project decision that departs from S-15's recommended value, for the localhost reason given.
- **Verification:** An integration test checks the headers on `/` and on one API route, and checks that `X-Powered-By` and `Strict-Transport-Security` are absent.

**SC-008 — Content Security Policy**
- **Status:** ACTIVE
- **Rule:** The HTML shell MUST be served with `default-src 'none'; script-src 'self'; style-src 'self'; img-src 'self'; font-src 'self'; connect-src 'self'; base-uri 'none'; form-action 'self'; frame-ancestors 'none'; object-src 'none'`. The build MUST NOT need `'unsafe-inline'` or `'unsafe-eval'`.
- **Enforcement:** Gin middleware that serves the embedded SPA; Vite build output.
- **Evidence:** S-14, the basic policy and `frame-ancestors`. `font-src 'self'` comes from DESIGN.md (self-hosted fonts). `frame-ancestors 'none'` is a project decision that is stricter than the source.
- **Verification:**
  - The header is present on the page.
  - Injecting an inline `<script>` in a dev test is blocked, and a CSP violation appears in the console.
  - The built `index.html` contains no inline script.

### Input validation and data access

**SC-010 — Strict JSON input**
- **Status:** ACTIVE
- **Rule:** API handlers MUST decode into typed structs and reject unknown fields. Each field MUST be validated for type, length, and allowed values (enums such as risk, channels, and days; IANA time zone; `HH:MM` time) before domain code sees it. Validation failures MUST return 400.
- **Enforcement:** HTTP API edge (TB-1); the domain re-checks business rules (DR-2).
- **Evidence:** S-06 (`BindJSON` aborts with 400); S-18 V2. Rejecting unknown fields is a project decision.
- **Verification:** A body with an extra field, a risk of `"Severe"`, or a time zone of `"Mars/Base"` returns 400 and changes nothing.

**SC-011 — Parameterized SQL only**
- **Status:** ACTIVE
- **Rule:** All SQL MUST use pgx positional placeholders (`$1`…) for values. Dynamic identifiers, such as sort columns, MUST come from a fixed server-side allowlist. String concatenation of input into SQL MUST NOT occur, and multi-statement simple-protocol queries MUST NOT be used.
- **Enforcement:** The storage layer.
- **Evidence:** S-07, placeholders, `Identifier`, and the simple-protocol warning. The allowlist is a project decision.
- **Verification:**
  - A keyword search for `' OR 1=1 --` returns only stories that contain that literal text.
  - A sort parameter of `title; DROP TABLE stories` returns 400.
  - A lint or grep check finds no `fmt.Sprintf` producing SQL.

**SC-012 — Keyword search uses safe full-text functions**
- **Status:** ACTIVE
- **Rule:** FR-5.5 search MUST pass user text to `websearch_to_tsquery` or `plainto_tsquery` as a bound parameter, and MUST cap the input at 200 characters.
- **Enforcement:** Story store.
- **Evidence:** FR-5.5; ARCHITECTURE.md (PostgreSQL full-text search); S-07. The function choice and cap are project decisions.
- **Verification:** Search input with tsquery operators (`&|!:*`) does not raise a database error. A 201-character query returns 400.

**SC-013 — Slack webhook URL validation**
- **Status:** ACTIVE
- **Rule:** A saved webhook MUST parse as an `https` URL with host exactly `hooks.slack.com` and path prefix `/services/`, with no userinfo, port, query, or fragment. Anything else MUST be rejected.
- **Enforcement:** Alerting domain on save (FR-4.16); re-checked by the Slack adapter before each send.
- **Evidence:** FR-4.16; S-27 (URL format). The host allowlist is a project decision; GovSlack is excluded.
- **Verification:** `https://hooks.slack.com.evil.example/services/x`, `http://hooks.slack.com/services/x`, and `https://hooks.slack.com@10.0.0.1/services/x` are each rejected. A valid URL is accepted.

**SC-014 — Phone number validation**
- **Status:** ACTIVE
- **Rule:** Phone numbers MUST be stored in E.164 form, checked against `^\+[1-9][0-9]{1,14}$`. Anything else MUST be rejected.
- **Enforcement:** Alerting domain.
- **Evidence:** FR-4.3, FR-4.15; S-18 V2. The format is a project decision.
- **Verification:** `5551234`, `+0123`, and `+1 555 123` are rejected. `+15551234567` is accepted.

**SC-015 — Admin source records**
- **Status:** ACTIVE
- **Rule:** A source address and license link MUST be absolute `https` URLs. The source MUST NOT be enabled until every FR-8.2 and FR-8.8 field is present.
- **Enforcement:** Source registry.
- **Evidence:** FR-8.2, FR-8.3, FR-8.8; S-16 (allowed schemes). Requiring `https` rather than `http` is a project decision.
- **Verification:** Saving `file:///etc/passwd` or `http://…` is rejected. Enabling a source without a license link fails.

### Collected content (TB-2) and outbound requests

**SC-020 — Outbound request guard (SSRF)**
- **Status:** ACTIVE
- **Rule:** The Collector and the Slack, Twilio, HIBP, and MITRE clients MUST share one `http.Client` with these protections:
  - a `net.Dialer` `Control` hook that rejects loopback, private, link-local, unique-local, multicast, unspecified, and IPv4-mapped forms of those addresses, at connect time
  - an overall `Timeout`
  - `CheckRedirect` that returns an error, so redirects are not followed
  - `http` and `https` schemes only
- **Enforcement:** Outbound HTTP adapter used by Collector and channel adapters.
- **Evidence:** S-16 (case 2 blocklist, connect-time check against rebinding, disable redirects, scheme allowlist).
- **Verification:**
  - A source pointed at `https://127.0.0.1/`, `https://[::ffff:10.0.0.1]/`, or a hostname resolving to `192.168.x.x` fails, and the failure is recorded (FR-1.11).
  - A 302 to a private IP is not followed.

**SC-021 — Feed size and time limits**
- **Status:** ACTIVE
- **Rule:**
  - Each fetched response MUST be read through `io.LimitReader` with a 10 MiB cap (project decision). Larger responses fail the collection.
  - Each fetch MUST run under a `context` deadline.
  - gofeed MUST be called with that size-limited reader through `ParseWithContext` or `Parse`. Its URL-fetching helper MUST NOT be used.
- **Enforcement:** Collector.
- **Evidence:** FR-1.10, FR-1.11; S-05 (the decoder has no size limit); S-16. The cap is a project decision.
- **Verification:** A test feed of 11 MiB fails with a recorded cause. Other sources still collect (FR-1.10).

**SC-022 — Normalize collected text to plain text**
- **Status:** ACTIVE
- **Rule:**
  - On intake, the Collector MUST convert titles, excerpts, and source-supplied names to plain text by removing markup and control characters, and MUST cap their lengths.
  - Item links MUST be absolute `http` or `https` URLs. Items with other link schemes MUST be dropped.
  - Stored content MUST NOT be stored or served as HTML.
- **Enforcement:** Collector (TB-2).
- **Evidence:** NFR-3.4; ARCHITECTURE.md TB-2; S-18 V1. Plain-text-only storage is a project decision (DESIGN.md: "render as plain text").
- **Verification:** An item titled `<img src=x onerror=alert(1)>` is stored without markup. An item linking to `javascript:alert(1)` is dropped.

**SC-023 — Content rights single gate**
- **Status:** ACTIVE
- **Rule:** Every output path (API story responses, email, Slack, SMS) MUST get the displayable fields of a story from the single Source registry function. No other code path MAY read stored excerpt text for output.
- **Enforcement:** Source registry (DR-4).
- **Evidence:** FR-8.8, FR-8.9, FR-1.17, FR-1.20, FR-1.21; ARCHITECTURE.md DR-4. This is a project decision, not a public-source control.
- **Verification:** For a "headline and link only" source, the API, email, and Slack outputs contain no excerpt. For a Reddit item, they contain no category or scores.

**SC-024 — Untrusted STIX data**
- **Status:** ACTIVE
- **Rule:** The ATT&CK bundle MUST be loaded from a pinned file with a recorded SHA-256 hash. It MUST be parsed into typed structs, and only technique IDs matching `^T\d{4}(\.\d{3})?$` MUST be accepted. Links MUST be built by the server as `https://attack.mitre.org/techniques/…`. URLs from the bundle MUST NOT be used.
- **Enforcement:** Analyzer.
- **Evidence:** FR-1.4, FR-7.1, FR-7.2; S-18 V15. This is a project decision.
- **Verification:** A bundle with a modified hash is refused at load. A technique ID of `T1190"><x` is ignored.

### Output encoding and the client

**SC-030 — Bounded concurrency and deadlines**
- **Status:** ACTIVE
- **Rule:** Every outbound call and database query MUST carry a `context` deadline. Job workers (Collector, Alerting) MUST use a fixed-size worker pool. Unbounded goroutines per item MUST NOT be spawned.
- **Enforcement:** Scheduler and jobs.
- **Evidence:** NFR-2.2; S-02 (timeouts); S-18 V15. The pool design is a project decision.
- **Verification:** A test source that never responds times out within its deadline, and the alert run still completes on time.

**SC-031 — HTML email uses html/template**
- **Status:** ACTIVE
- **Rule:**
  - Email HTML bodies MUST be rendered with `html/template`. `text/template` and string concatenation MUST NOT be used for HTML.
  - Values MUST NOT be passed as `template.HTML`, `template.URL`, or similar trusted types.
  - The email MUST contain no scripts, images, or remote resources, and MUST include a plain-text part.
- **Enforcement:** Alerting email renderer.
- **Evidence:** NFR-3.4; DESIGN.md (email alert); ARCHITECTURE.md TB-2. The source is the `html/template` package documentation (contextual escaping), which was not separately fetched; the design rule is a project decision.
- **Verification:** A story titled `<script>x</script>` appears escaped in the HTML part. A grep finds no `template.HTML(` in email code.

**SC-032 — Email header injection**
- **Status:** ACTIVE
- **Rule:** Recipient, subject, and every header value MUST be rejected or stripped if they contain CR or LF. Recipients MUST be parsed with `net/mail.ParseAddress`.
- **Enforcement:** Email adapter.
- **Evidence:** FR-4.2, FR-6.9; S-18 V1. This is a project decision.
- **Verification:** A subject containing `\r\nBcc: x@example.org` does not add a header.

**SC-033 — SMTP requires TLS**
- **Status:** ACTIVE
- **Rule:** The email adapter MUST NOT use `smtp.SendMail`. It MUST use either implicit TLS (`tls.Dial`, port 465) or `smtp.Client.StartTLS`, and MUST fail the send if STARTTLS is not offered. Certificates MUST be verified.
- **Enforcement:** Email adapter.
- **Evidence:** S-03 (`SendMail` upgrades only "if possible"; `PlainAuth` refuses non-TLS).
- **Verification:** Against a test SMTP server without STARTTLS, the send fails and records the failure (FR-4.19).

**SC-034 — Slack text escaping**
- **Status:** ACTIVE
- **Rule:** All story text in Slack payloads MUST have `&`, `<`, and `>` escaped as `&amp;`, `&lt;`, and `&gt;` before it is embedded. Links MUST be built only from SC-022-validated URLs. The payload MUST be built with `encoding/json`.
- **Enforcement:** Slack adapter.
- **Evidence:** S-28 (escaping); NFR-3.4.
- **Verification:** A title `<!channel> <https://evil|x>` arrives as literal text and does not notify the channel.

**SC-040 — No raw HTML in React**
- **Status:** ACTIVE
- **Rule:** The client MUST NOT use `dangerouslySetInnerHTML`, `eval`, `new Function`, or direct `innerHTML` writes. All story fields MUST render as React text children.
- **Enforcement:** React client; a build-time grep check.
- **Evidence:** S-19 (React does not sanitize `dangerouslySetInnerHTML`); NFR-3.4; DESIGN.md. Banning it completely is a project decision.
- **Verification:**
  - A CI grep for `dangerouslySetInnerHTML|innerHTML|eval\(|new Function` fails the build.
  - A story title of `<b>x</b>` renders as visible tags.

**SC-041 — Safe links in the client**
- **Status:** ACTIVE
- **Rule:** Before rendering, the client MUST parse every external `href` with `new URL()` and render it only when the protocol is `http:` or `https:`. External links MUST use `rel="noopener noreferrer"`.
- **Enforcement:** One shared React link component.
- **Evidence:** NFR-3.4; DESIGN.md (destination domain shown); S-18 V3. The client check is a project decision that adds defense in depth to SC-022, because React's handling of `javascript:` was not verified.
- **Verification:** A component test with `javascript:alert(1)` renders no anchor.

**SC-042 — Prototype-safe keyed data**
- **Status:** ACTIVE
- **Rule:** Client code that keys data by server-supplied strings (categories, sources, tactics) MUST use `Map` or `Set`, or objects created with `Object.create(null)`. It MUST NOT deep-merge untrusted JSON into objects.
- **Enforcement:** React client.
- **Evidence:** S-17 (Map/Set, `Object.create(null)`).
- **Verification:** A unit test loads a category named `__proto__`. It displays, and `({}).polluted` stays `undefined`.

**SC-043 — No secrets in the bundle; no source maps**
- **Status:** ACTIVE
- **Rule:**
  - No secret MAY be placed in a `VITE_`-prefixed variable, and `envPrefix` MUST NOT be changed.
  - `build.sourcemap` MUST stay `false` for the embedded build.
  - The Vite dev server MUST keep `server.host` set to `localhost` and the default `server.fs` settings, MUST NOT set `allowedHosts: true`, and MUST NOT set `server.cors: true`.
- **Enforcement:** `vite.config.ts`; review.
- **Evidence:** S-20, S-21, S-22.
- **Verification:**
  - The built bundle contains no Twilio SID, SMTP password, or `.env` value (grep).
  - `dist/` contains no `.map` files.
  - The config test asserts host and cors.

**SC-044 — TypeScript strict**
- **Status:** ACTIVE
- **Rule:** `tsconfig.json` MUST set `"strict": true`, and `tsc --noEmit` MUST pass before a build.
- **Enforcement:** Toolchain (ARCHITECTURE.md Toolchain).
- **Evidence:** ARCHITECTURE.md (TypeScript catches rendering mistakes). Setting it explicitly is a project decision, because the TS 7 default was not verified.
- **Verification:** A file with an implicit `any` fails the type-check.

### Authentication (Identity)

**SC-050 — Password hashing**
- **Status:** ACTIVE
- **Rule:**
  - Passwords MUST be hashed with argon2id at no less than m=19456 KiB, t=2, p=1, with a 16-byte random salt per hash from `crypto/rand` and a 32-byte output.
  - Parameters MUST be stored with each hash.
  - Comparison MUST use `subtle.ConstantTimeCompare`.
- **Enforcement:** Identity.
- **Evidence:** S-10, Argon2id. The salt and output lengths are project decisions.
- **Verification:** A stored hash string shows `m=19456,t=2,p=1`. Two accounts with the same password have different hashes.

**SC-051 — Password acceptance**
- **Status:** ACTIVE
- **Rule:**
  - Passwords MUST be at least 12 characters, counting Unicode code points.
  - Passwords of at least 64 characters MUST be accepted. The maximum is 256 (project decision).
  - Passwords MUST NOT be truncated, and composition rules MUST NOT be imposed.
  - A password found in HIBP (count > 0) MUST be rejected.
- **Enforcement:** Identity, on set, reset, and change.
- **Evidence:** FR-6.6; S-11 §3.1.1.2 (no composition rules, no truncation, allow ≥64, blocklist). The 12-character minimum comes from FR-6.6.
- **Verification:**
  - An 11-character password is rejected.
  - A 64-character passphrase is accepted.
  - `Password1234` is rejected as breached.

**SC-052 — HIBP range lookup**
- **Status:** ACTIVE
- **Rule:**
  - The breach check MUST send only the first 5 hex characters of the SHA-1 to `https://api.pwnedpasswords.com/range/{prefix}`, with `Add-Padding: true`.
  - Padded zero-count entries MUST be ignored.
  - If the API is unreachable, the password MUST be refused (fail closed).
- **Enforcement:** Identity, through the SC-020 client.
- **Evidence:** S-26; ARCHITECTURE.md AQ-6 (fail closed).
- **Verification:** A mock asserts the request path is 5 characters and the header is present. With the network blocked, setting a password fails with a "try again later" message.

**SC-053 — TOTP verification**
- **Status:** ACTIVE
- **Rule:**
  - TOTP MUST be checked with `totp.ValidateCustom` using Period 30, Digits 6, SHA1, and Skew 1, set explicitly.
  - The last accepted time step MUST be stored per account, and a code for that step or an earlier one MUST be rejected.
  - TOTP secrets MUST be generated with at least 160 bits.
- **Enforcement:** Identity.
- **Evidence:** FR-6.5, FR-6.15; S-08 (Validate defaults; no replay protection); S-11 (an OTP is accepted only once). Explicit parameters are a project decision.
- **Verification:** The same valid code used twice within 30 seconds fails the second time with the generic error (FR-6.8).

**SC-054 — Uniform login failure and lockout**
- **Status:** ACTIVE
- **Rule:**
  - Every login failure MUST return the single DESIGN.md message: wrong email, wrong password, wrong code, locked account, or disabled account.
  - The password hash check MUST run even for unknown emails, using a dummy hash.
  - After 5 failures in 15 minutes, the account MUST be blocked for 15 minutes.
- **Enforcement:** Identity.
- **Evidence:** FR-6.3, FR-6.7, FR-6.8, FR-9.4; DESIGN.md (lockout). The dummy hash is a project decision.
- **Verification:**
  - The responses for an unknown email and for a wrong password are byte-identical, and their timing is within the same order.
  - The sixth attempt with correct credentials inside the window fails.

**SC-055 — Password reset tokens**
- **Status:** ACTIVE
- **Rule:**
  - Reset tokens MUST come from `crypto/rand.Text()` and be stored only as a SHA-256 hash.
  - A token MUST be single-use and expire in 30 minutes.
  - Using a token MUST invalidate all of the account's sessions and all its other tokens.
  - The request endpoint MUST always give the same response.
- **Enforcement:** Identity.
- **Evidence:** FR-6.9; DESIGN.md (reset message); S-04 (`Text`); S-12 (invalidate on credential change). Hashing tokens and invalidating sessions are project decisions.
- **Verification:**
  - A token used twice fails the second time.
  - A token used at minute 31 fails.
  - A session open before the reset is rejected afterwards.

**SC-056 — Phone verification codes**
- **Status:** ACTIVE
- **Rule:**
  - Codes MUST be 6 digits from `crypto/rand` and MUST be stored only as a hash.
  - They MUST be compared in constant time and MUST expire after 10 minutes.
  - A code MUST be invalidated after 5 wrong entries.
  - A new code MUST invalidate the previous one. *(delegated decision)*
- **Enforcement:** Alerting domain.
- **Evidence:** FR-4.15; S-04. The limits are project decisions.
- **Verification:**
  - A correct code entered at minute 11 fails.
  - A correct code entered after 5 wrong entries fails.
  - The first code fails after a second code is sent.

**SC-057 — TOTP loss and recovery**
- **Status:** ACTIVE
- **Rule:**
  - The only recovery path is an admin resetting another account's TOTP. The reset MUST delete the TOTP secret, end all of that account's sessions, write an audit row, and force TOTP setup at the next login (FR-6.15).
  - An admin MUST NOT reset their own TOTP through the web.
  - If the last admin loses their device, recovery MUST use the local install CLI (TB-5).
  - There are no recovery codes. No other path MAY skip TOTP. *(delegated decision)*
- **Enforcement:** Identity; installer CLI.
- **Evidence:** FR-6.5, FR-6.15, FR-9.6; ARCHITECTURE.md TB-5; S-11; S-12 (invalidate sessions on credential change).
- **Verification:**
  - After an admin reset, the target's old session returns 401, and the next login requires enrolment.
  - A user-role request to the reset route returns 403.
  - An admin's reset of their own TOTP returns 403.

**SC-058 — Request rate limits**
- **Status:** ACTIVE
- **Rule:** Per account and per rolling hour, the system MUST allow at most:
  - 3 password-reset emails
  - 3 phone-code SMS
  - 5 Slack test sends
  
  Over-limit reset requests MUST still return the same generic response (SC-055) and MUST NOT send. *(delegated decision)*
- **Enforcement:** Identity and Alerting domain, with counts stored in PostgreSQL.
- **Evidence:** FR-4.15, FR-4.17, FR-6.9; S-18 V2. The limits are project decisions.
- **Verification:** The fourth reset request in an hour returns the generic response, and the mock SMTP server receives no fourth email.

### Sessions, CSRF, and authorization

**SC-060 — Session identifiers and cookie**
- **Status:** ACTIVE
- **Rule:**
  - Session IDs MUST come from `crypto/rand.Text()` and be stored server-side as a SHA-256 hash.
  - The cookie MUST be `__Host-gmb_session` with `Secure; HttpOnly; SameSite=Strict; Path=/` and no `Domain`.
- **Enforcement:** HTTP API session middleware; Identity.
- **Evidence:** S-12 (Cookies, Cookie name prefixes, entropy); S-04. Storing the hash is a project decision.
- **Verification:** The `Set-Cookie` header matches exactly. A database dump shows no raw session ID.

**SC-061 — Session lifecycle**
- **Status:** ACTIVE
- **Rule:**
  - A new session ID MUST be issued after full login (password plus TOTP) and after a role change. The previous session MUST be destroyed.
  - Sessions MUST end server-side after 30 minutes idle, after 8 hours in total (absolute timeout, *delegated decision*), and at logout.
  - Disabling or deleting an account MUST end its sessions.
- **Enforcement:** Identity.
- **Evidence:** FR-6.10, FR-9.4; S-12 (renew ID, idle timeout, absolute timeout).
- **Verification:**
  - The cookie value before login is different after login, and the old value is rejected.
  - After 31 idle minutes, a request returns 401.
  - A session kept active for 8 hours and 1 minute returns 401.
  - Logout followed by replaying the old cookie returns 401.

**SC-062 — Partial-login state**
- **Status:** ACTIVE
- **Rule:**
  - A session that has passed the password but not TOTP, or that still needs TOTP setup (FR-6.15), MUST reach only the TOTP endpoints. It MUST expire after 5 minutes (project decision).
  - The client UI MUST NOT be the gate.
- **Enforcement:** HTTP API middleware.
- **Evidence:** FR-6.5, FR-6.15; DESIGN.md (setup hides navigation); S-12.
- **Verification:** With a password-only session, `GET /api/stories` returns 401.

**SC-063 — CSRF protection**
- **Status:** ACTIVE
- **Rule:**
  - All routes MUST be wrapped in `http.CrossOriginProtection`. Trusted origins MUST NOT be added, and bypass patterns MUST NOT be configured.
  - State-changing API requests MUST also require a custom header `X-GMB-CSRF: 1` and `Content-Type: application/json`.
  - GET MUST NOT change state.
- **Enforcement:** HTTP API middleware (TB-1).
- **Evidence:** S-02 (`CrossOriginProtection`, go1.25+); S-13 (custom header / disallow simple requests, Fetch Metadata, no state change on GET); SC-060 SameSite as defense in depth.
- **Verification:**
  - A POST with `Sec-Fetch-Site: cross-site` returns 403.
  - A POST without the custom header returns 403.
  - A cross-origin form POST does nothing.

**SC-064 — Server-side authorization on every handler**
- **Status:** ACTIVE
- **Rule:**
  - Every route except login, TOTP, and reset MUST require an authenticated session.
  - Admin routes MUST check the admin role in Identity.
  - Per-user settings MUST take the user ID from the session, never from the request.
  - Denials MUST return 403 or 404 without revealing whether the target exists.
- **Enforcement:** Identity, called by every handler (TB-1); a route-table test.
- **Evidence:** FR-6.1, FR-6.2, FR-6.12, FR-6.13, FR-6.14, FR-8.1, FR-9.1; ARCHITECTURE.md TB-1, DR-2.
- **Verification:**
  - A test enumerates all routes. Unauthenticated access returns 401. A user-role session on admin routes returns 403.
  - User A's request carrying user B's ID changes only A's settings.

**SC-065 — Admin safety rules**
- **Status:** ACTIVE
- **Rule:**
  - Identity MUST refuse removing the role from, or disabling, the last active admin.
  - Account deletion MUST remove the email, phone, and webhook in the same transaction.
  - Each admin action MUST write an append-only audit row in the same transaction.
- **Enforcement:** Identity; Audit log.
- **Evidence:** FR-9.3, FR-9.5, FR-9.6; ARCHITECTURE.md (append-only audit). This is a project decision.
- **Verification:**
  - Demoting the only admin through the API fails even when the UI is bypassed.
  - After a deletion, the contact data is gone and an audit row exists.
  - The app's database role cannot `UPDATE` or `DELETE` audit rows.

**SC-066 — First admin bootstrap**
- **Status:** ACTIVE
- **Rule:** The first admin MUST be created only by a local CLI command, never over HTTP. The command MUST refuse to run if any admin already exists.
- **Enforcement:** Installer CLI (TB-5).
- **Evidence:** FR-9.7, FR-9.2; ARCHITECTURE.md TB-5.
- **Verification:** No HTTP route creates accounts without an admin session. Running the CLI twice fails the second time.

### Secrets, data, and the database

**SC-070 — Secrets never leave the server**
- **Status:** ACTIVE
- **Rule:** API responses, logs, and errors MUST NOT contain password hashes, TOTP secrets (after enrolment), webhook URLs, phone codes, reset tokens, session IDs, or provider credentials.
- **Enforcement:** Domain-to-API mapping (DR-6); slog redaction (SC-080).
- **Evidence:** NFR-3.3; ARCHITECTURE.md DR-6; S-27 (the webhook URL "contains a secret").
- **Verification:** After saving a webhook, `GET` settings shows only "saved". A log grep for `hooks.slack.com` finds nothing.

**SC-071 — Secrets at rest**
- **Status:** ACTIVE
- **Rule:**
  - TOTP secrets and Slack webhook URLs MUST be encrypted in PostgreSQL with AES-256-GCM (Go `crypto/aes` + `crypto/cipher`). Each value MUST use a random 96-bit nonce, and the account ID MUST be bound as associated data.
  - The 256-bit data key, the SMTP app password, and the Twilio key secret MUST live in one `0600` secrets file outside the repository and outside the PostgreSQL data directory (SC-075).
  - Secrets MUST NOT be committed to the repository, passed on the command line, or placed in environment variables visible to other users.
  - The owner's disk SHOULD use full-disk encryption. *(delegated decision)*
- **Enforcement:** Identity and Alerting (field encryption); startup secrets loader.
- **Evidence:** NFR-3.3; ARCHITECTURE.md TB-4; S-27 (webhook URL is a secret); S-29; S-18 V11, V14. The mechanism is a project decision.
- **Verification:**
  - A `git log -p` secret scan is clean.
  - A database dump shows no `hooks.slack.com` text and no base32 TOTP secrets.
  - Copying a ciphertext to another account's row fails to decrypt.

**SC-072 — Twilio credential scope**
- **Status:** ACTIVE
- **Rule:** The SMS adapter MUST authenticate with a Twilio Standard or Restricted API key, not the Account SID with the Auth Token and not a Main key.
- **Enforcement:** SMS adapter configuration.
- **Evidence:** S-29 (API keys preferred; key types).
- **Verification:** The configured credential's SID starts with `SK`, and the key type in the Twilio console is not Main.

**SC-073 — PostgreSQL access**
- **Status:** ACTIVE
- **Rule:**
  - PostgreSQL MUST listen on localhost only and MUST authenticate with `scram-sha-256`. `md5` and `trust` MUST NOT appear in `pg_hba.conf`.
  - The app MUST connect as a role that owns no schema objects and has only the needed DML grants.
  - libpq `sslkeylogfile` MUST NOT be set.
- **Enforcement:** Database setup (TB-4).
- **Evidence:** S-09 (MD5 deprecated in PostgreSQL 18; `sslkeylogfile`); ARCHITECTURE.md TB-4.
- **Verification:**
  - `SHOW listen_addresses` returns `localhost`.
  - `pg_hba.conf` contains no `md5` or `trust`.
  - The app role's attempt to run `DROP TABLE` fails.

**SC-074 — Data minimization and deletion**
- **Status:** ACTIVE
- **Rule:**
  - Contact data MUST be read only by the Alerting and Identity (reset) paths.
  - Retention MUST delete stories after 365 days and delivery records after 90 days.
  - Reddit removals MUST be applied within 48 hours.
- **Enforcement:** Retention job; Collector; Identity.
- **Evidence:** NFR-3.2, FR-10.1, FR-10.2, FR-1.18, FR-9.5. This is a project decision.
- **Verification:** After the retention job runs, seeded records older than each limit are gone and newer ones remain.

**SC-075 — Process and file permissions**
- **Status:** ACTIVE
- **Rule:**
  - The server MUST run as an unprivileged OS user, not root.
  - Configuration and secret files MUST be mode `0600`, owned by that user.
  - The server MUST refuse to start if a secret file is readable by group or others.
  - The code MUST NOT use `os/exec` or `unsafe`.
- **Enforcement:** Startup check; CI grep.
- **Evidence:** ARCHITECTURE.md TB-4 ("only the server process reads the secrets"); S-18 V13. This is a project decision.
- **Verification:**
  - Starting with a `0644` secret file exits with an error.
  - A grep for `"os/exec"` or `"unsafe"` finds nothing.

### Errors and logging

**SC-080 — Structured, redacted logging**
- **Status:** ACTIVE
- **Rule:**
  - Logs MUST use `log/slog` with `JSONHandler`.
  - Types that hold secrets or contact data MUST implement `slog.LogValuer` and return a redacted value.
  - Untrusted strings MUST be logged only as attribute values, never inside the message key.
- **Enforcement:** Logging setup; all components.
- **Evidence:** ARCHITECTURE.md (`log/slog`); S-18 V16. JSON output and LogValuer redaction are project decisions; the slog documentation was not separately fetched.
- **Verification:**
  - Logging an account struct shows `"[redacted]"` for phone and webhook.
  - A source error containing `\n{"level":"ERROR"}` appears as one escaped value.

**SC-081 — Security events logged**
- **Status:** ACTIVE
- **Rule:** The following MUST be logged with time, account ID, and outcome, without credentials:
  - login success and failure
  - lockout
  - TOTP enrolment
  - password reset request and use
  - logout
  - authorization denials
  - admin actions
  - collection and delivery failures
- **Enforcement:** Identity, HTTP API, Collector, Alerting.
- **Evidence:** FR-1.11, FR-4.19, FR-9.6; S-18 V16.
- **Verification:** A failed login produces exactly one log entry with `outcome=failure` and no password field.

**SC-082 — Generic error responses**
- **Status:** ACTIVE
- **Rule:**
  - Panics MUST be recovered by middleware.
  - The client MUST get a generic message and a random correlation ID only, never a stack trace, SQL error, internal ID, or file path.
  - Details MUST go to the log under the same correlation ID.
- **Enforcement:** Gin recovery middleware; error mapper.
- **Evidence:** DESIGN.md ("What errors may reveal"); S-18 V16.
- **Verification:** A handler forced to panic returns 500 with a body that has no `goroutine` or `.go:` text, and the log has the stack.

**SC-083 — Log retention**
- **Status:** ACTIVE
- **Rule:** Application logs MUST be written to a directory with mode `0700`, owned by the server's OS user, outside the repository. Logs MUST be rotated daily, and log files older than 30 days MUST be deleted. *(delegated decision)*
- **Enforcement:** Logging setup; Retention job.
- **Evidence:** NFR-3.2; S-18 V16. The values are project decisions.
- **Verification:**
  - The log directory is `0700`.
  - After the Retention job runs, a seeded 31-day-old log file is gone and a 29-day-old file remains.

### Dependencies and build

**SC-090 — Supported toolchains**
- **Status:** ACTIVE
- **Rule:**
  - The server MUST be built with a Go release that is still supported (one of the two newest majors), pinned with the `toolchain` directive in `go.mod`.
  - The client MUST be built with an Active or Maintenance LTS Node.js release.
  - PostgreSQL MUST be a supported major version.
- **Enforcement:** `go.mod`; build machine.
- **Evidence:** S-01 (support policy); S-25 (production uses LTS only); ARCHITECTURE.md (PostgreSQL 18 supported until 2030-11-14).
- **Verification:** `go version` matches the `go.mod` toolchain line. `node -v` is in an LTS line on S-25.

**SC-091 — Locked, verified dependencies**
- **Status:** ACTIVE
- **Rule:**
  - Each PROPOSED package (pgx, pquerna/otp, gofeed, Vitest, and others) MUST be pinned, when first added, to its latest tagged release that passes SC-092. The pinned version MUST be recorded in ARCHITECTURE.md. *(delegated decision)*
  - `go.sum` and `package-lock.json` MUST be committed.
  - Client installs MUST use `npm ci --ignore-scripts`, and `npm audit signatures` MUST pass.
  - No dependency MAY be added outside ARCHITECTURE.md's stack without a new decision.
- **Enforcement:** Toolchain and CI.
- **Evidence:** S-23 (`npm ci`, `ignore-scripts`); S-24 (audit signatures); ARCHITECTURE.md (Stack).
- **Verification:**
  - Changing `package.json` without updating the lockfile makes `npm ci` fail.
  - A tampered `go.sum` entry fails `go mod verify`.

**SC-092 — Vulnerability audit gate**
- **Status:** ACTIVE
- **Rule:** `govulncheck ./...` and `npm audit --omit=dev` MUST pass, with no known-exploitable findings, before a build is installed. Any exception MUST be recorded with a reason and a date.
- **Enforcement:** Toolchain (ARCHITECTURE.md Toolchain table).
- **Evidence:** ARCHITECTURE.md Toolchain; S-24.
- **Verification:** Pinning a dependency with a known advisory in a test branch makes the gate fail.

## Open Security Decisions

None. OD-001 to OD-008 were resolved by delegated decision (the owner told the author to answer all open questions). The answers are recorded in SC-002, SC-007, SC-056, SC-057, SC-058, SC-061, SC-071, SC-083, and SC-091, and marked *(delegated decision)*. Still UNKNOWN, but no rule depends on them: the OS of the owner's machine and the SMTP provider (ARCHITECTURE.md).
