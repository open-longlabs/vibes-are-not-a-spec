# Rules

Paste these together with any playbook.

```
Rules for this audit.
Inventory before judging, judge before fixing.
For security playbooks, write an access matrix first: who may do what with which data
(anyone, logged-in user, owner, team, admin, signed webhook, job); if my intent is
unclear, ask, don't assume owner-only.
For implementation claims cite file:line; for behaviour claims save the command or
browser steps, the actual result, the environment and the artifact path.
Use test accounts and synthetic data.
Before saving or reporting evidence, redact passwords, keys, tokens, cookies, connection
strings and personal data; identify a leaked secret by location and key type, never by
value.
A code citation alone cannot prove behaviour.
PASS applies only to the scenario and environment actually exercised.
Check which browser, runtime and test tools exist first; if one is missing, mark the
affected checks NOT RUN.
Never invent runs, screenshots, users or results.
Status per check: FAIL, PASS (with how you checked), NOT APPLICABLE (with why),
UNVERIFIED (with what I must check and where), NOT RUN (never counts as PASS).
Only I can mark something ACCEPTED.
Exercise the actual application logic and never stub the behaviour being asserted; use
sandbox services or labelled fakes for unsafe external effects and leave untested
provider behaviour UNVERIFIED; security tests run as real low-privilege users
(anonymous, user A, user B), never with an admin or service key.
In security tests, every denied test gets an allowed twin that succeeds and every denied
write is followed by proof nothing changed.
Fix highest severity first, one change at a time, re-run the proof after each.
Abuse and destructive tests only on local or staging with test data.
Never deploy, merge, delete production data, change DNS, rotate keys or print secrets
yourself: give me the exact steps.
You may create and remove clearly identified test fixtures on local or staging.
Don't swap the stack or add paid services without asking.
P0 means ongoing severe harm or a core service down, P1 a core task blocked or real user
harm, P2 a lesser defect; taste is a recommendation, not a failure.
After 5 fixes, checkpoint progress and remaining risks; revert an unsuccessful change of
yours without touching unrelated work; a playbook's own limit takes precedence.
Report: findings (severity, proof, status), changes per file, tests with before and
after, what I must do, what you couldn't check.
```
