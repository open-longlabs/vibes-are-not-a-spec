# API LARP

You say: protect my API, lock down my backend

Paste this together with the [rules](00-rules.md) into your coding agent.

```
API LARP.
Assume every backend entry point can be abused until a request proves otherwise.
Inventory every callable surface, not just /api: route handlers, server actions, edge
functions, client-callable RPC or database functions, webhooks, cron and jobs, each with
method, path, file:line, who may call it, what it reads or changes, which fields it
accepts and returns.
Then probe:

(1) as user A, read, list, change and delete user B's object by swapping the ID in URL,
    body and query;
(2) call protected surfaces with no session, an expired one and a tampered one and check
    no work happens before the check (public routes and signed webhooks keep their own
    correct check);
(3) responses leaking fields the caller shouldn't see and requests that set role, owner,
    plan, credits or price by adding them, nested objects included;
(4) no numeric limit on requests, page size, body size or time for expensive calls (AI,
    email, uploads) and limits held in memory on serverless;
(5) admin actions callable by a normal user because the check lives only in the UI;
(6) one-time benefits (coupon, trial, invite, credits) redeemed twice by two
    simultaneous requests;
(7) server fetching a user-supplied URL that can reach localhost, 169.254.169.254,
    private ranges or IPv6 equivalents, including via redirects;
(8) stack traces, SQL errors or debug routes in responses;
(9) forgotten test, seed or old routes still live;
(10) webhooks or third-party responses used without signature check or validation;
(11) user input reaching SQL, shell or templates as code.

For each finding: severity (P0/P1/P2), the exact request and response that prove it, the
fix at the point the data is accessed (caller from the verified session, never the body;
field allowlists in and out; server-side role checks; limits in a shared store;
signature on the raw body; resolved-address checks for fetches; bound parameters) and
the guardrail that stops it coming back: an automated test with its allowed twin.
Re-run the proving request after each fix.
```

**What it covers:** someone changing an ID and seeing your users' data, making themselves admin with one extra field, using your app for free, running up your AI bill, or making your server fetch internal addresses. These are the OWASP API Security Top 10 (2023), plus injection.
**Sources:** [OWASP API Security Top 10, 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/) · [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) · [OWASP SSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) · [OWASP SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html) · [Stripe webhooks](https://docs.stripe.com/webhooks)
