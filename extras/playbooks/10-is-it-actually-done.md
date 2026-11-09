# LARP check

You say: is it actually done, is it done, did it work, are you sure

Paste this together with the [rules](00-rules.md) into your coding agent.

```
LARP check.
Run this after any task you told me is done.
Assume nothing works until it is proven.
Go through everything you changed or claimed and check:

(1) functions returning hardcoded or sample data instead of the real thing;
(2) tests that mock the logic they test, always pass, were skipped, or were edited to
    pass;
(3) try/catch or fallbacks that swallow errors and hide failure;
(4) validation, permission or signature checks that exist but never run on the real
    path, or only in the UI;
(5) async calls never awaited or checked;
(6) code paths, commands or migrations written but never executed;
(7) secrets or deployment-specific config hardcoded where it should come from the
    environment; intentional public URLs, constants and test fixtures are fine;
(8) words in your summary ("tested", "secure", "faster", "fixed") with no command
    output, test result or measurement behind them;
(9) parts of my request skipped, simplified or postponed without saying so;
(10) queries without limits, loops without an end, requests without timeouts.

For each: what you claimed, what you found, the evidence (file:line, the command and its
real output) and the Rules status.
Add REAL only for a claim supported by evidence, LARP for a contradicted or unsupported
claim.
Never upgrade to REAL without evidence.
Then fix every LARP item, most serious first, one at a time, show the real output after
each fix and give me the corrected summary.
```

**What it covers:** your AI saying "done, everything works" when it isn't: fake data, fake tests, swallowed errors, checks that never run, steps it quietly skipped.
**Why it exists:** when we ran this kind of check on our own database playbook, it found two factual errors we had written ourselves.
**Based on:** our practice of checking completion claims against observed behaviour and saved evidence.
