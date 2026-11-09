# Edge & Headers LARP

You say: add security headers, fix the security warnings

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Edge & Headers LARP.
Assume the edge leaks until a request proves otherwise.
List production and preview URLs.
Use curl -sS -I for first header checks on the home page, the login page and one API
route, then test the real GET or API method where behaviour matters, with a test session
and a browser for cookies, CORS, caching and redirects.
Abuse tests only on local or staging.
Check:

(1) http serves content without upgrading to https (check the redirect destination;
    prefer a permanent redirect), or an https page lacks HSTS;
(2) on HTML pages, CSP missing or allowing 'unsafe-eval' or *, no object-src 'none', no
    base-uri, no frame-ancestors, judged by actual effect; JSON API responses don't need
    a document CSP;
(3) X-Content-Type-Options nosniff, Referrer-Policy or Permissions-Policy missing;
(4) an unapproved origin (send Origin: https://evil.example and Origin: null) can read a
    private response in a real browser with credentials; report * with credentials as an
    invalid configuration and separately prove whether private data is readable;
(5) request concrete paths for secret files, backups and debug endpoints (/.env,
    /.git/config, /.DS_Store, source maps, .bak, .sql, .zip, /admin, /debug, API docs,
    GraphQL introspection), inspect the content and follow redirects; FAIL only when an
    unauthorized caller gets sensitive content or performs a protected action and record
    soft 404s separately;
(6) version numbers in Server or X-Powered-By, stack traces or framework error pages in
    production;
(7) session cookie without Secure, HttpOnly, SameSite, or scoped to the parent domain
    without need;
(8) /login?next=https://evil.example (and redirect=, returnUrl=) leaves the site;
(9) pages with personal data cached by the CDN or without Cache-Control: private,
    no-store;
(10) preview deployments public or on production keys and data, staging indexable;
(11) DNS records pointing at services we no longer use: list them, never touch DNS.

For each finding: severity (P0/P1/P2), the exact request and response that prove it, the
fix in the file that owns the config and the guardrail that stops it coming back: a line
in scripts/check-edge.sh that fails on it.
Fix highest severity first; prepare CSP as report-only, list what really loads, test it,
then prepare the enforcing config and give me the deployment steps; re-run the proving
request after each fix; click through the 3 main pages and check the console for CSP
errors; revert if anything breaks.
```

**What it covers:** everything between the internet and your app: HTTPS, the headers browsers use to protect your users, other sites calling your API with your users' cookies, files you never meant to publish (.env, .git, source maps), redirects used for phishing, private pages cached for strangers, forgotten subdomains someone else can take over.
**Check it yourself:** run your domain through [MDN HTTP Observatory](https://developer.mozilla.org/en-US/observatory) before and after.
**Sources:** [OWASP HTTP Headers](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html) · [OWASP REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html) · [OWASP Unvalidated Redirects](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) · [MDN CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) · [MDN HSTS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
