# Automation LARP

You say: make it automatic, automate this

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Automation LARP.
Assume every automation will fire twice, fail halfway and stop silently until a test
proves otherwise.
Before building or judging, write one row per automation: what triggers it, what goes
in, each step, what comes out, where the result is stored, who gets told, who owns it
and what it may cost.
Ask me for anything missing.
Then check:

(1) trigger: the exact event or schedule and what happens if it fires twice or two runs
    overlap;
(2) duplicates: for each email, payment, file or record, a stable key stored before
    sending, the provider's own duplicate protection where it exists and a plan for when
    the result is unknown (a timeout doesn't mean it didn't happen); test two copies at
    once and a failure right after the provider accepted;
(3) failure at each step: timeout set, retries capped with increasing delay and only
    steps that are safe to repeat get retried;
(4) half-finished runs: what state is left if step 3 of 5 fails and how it resumes or
    undoes;
(5) after the last retry: failed jobs go to a visible list and a named person is told;
(6) silent death: a scheduled job that doesn't run raises an alert;
(7) bad input: missing, malformed, huge or duplicate data stops cleanly before any side
    effect;
(8) permissions: each step has only the access it needs;
(9) cost: a hard cap on runs, items and AI spend and no loop without an end;
(10) keep routine automation I already authorised; require my approval, with a concrete
    preview, for new recipients, bulk or irreversible actions, or anything outside the
    approved templates, permissions and budget;
(11) records: every run has an ID and a log of input, steps, result and error, without
    secrets or personal data;
(12) control: a dry-run mode and an off switch I can use without a developer.

For each finding: severity, the file:line or run that proves it, the fix and the
guardrail: a test that replays a duplicate event, forces a failure at each step and
feeds bad input and records how many times each side effect actually happened in each
tested case.
Test with fake recipients and test payment keys only.
```

**What it covers:** the customer who gets the email twice, the job that died three weeks ago without anyone noticing, the half-sent update, the loop that burned your budget, the file that went nowhere and the stakeholder nobody told.
**Sources:** [Google SRE, handling overload and retries](https://sre.google/sre-book/handling-overload/) · [Google SRE, distributed periodic scheduling](https://sre.google/sre-book/distributed-periodic-scheduling/) · [Stripe, idempotent requests](https://docs.stripe.com/api/idempotent_requests) · [AWS Builders' Library, timeouts, retries and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/)
