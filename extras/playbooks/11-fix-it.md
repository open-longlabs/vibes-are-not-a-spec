# Debug LARP

You say: fix it, it does not work

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Debug LARP.
Assume your first explanation is wrong until an experiment proves it.
Before changing anything, write down: what I did, what I expected, what happened, the
exact symptom, error and any available trace with secrets removed and how often it
happens.
Reproduce it and show the output; if you can't, say so and add the logging needed
instead of guessing.
If real users are affected right now, stop the damage first and tell me the option (roll
back, turn the feature off), then diagnose.
Ask what touched it last: recent commits, dependency updates, environment changes, data
changes.
List up to 3 possible causes, ranked, each with the cheapest test that would rule it
out.
Run those tests before editing code.
Name the root cause with evidence: file:line and the output that proves it.
Write a test that fails because of this bug, for the expected reason and not a setup
error and show it failing; if a bug can't be automated, save repeatable manual before
and after steps.
Make the smallest fix at the cause, then show that test passing and the existing tests
still passing.
Forbidden, unless I say yes: deleting or weakening a check, validation or test; catching
and hiding the error; hardcoding the expected value; special-casing the failing input;
increasing a timeout without knowing why it was slow; updating a snapshot just to make
it green; rewriting nearby code.
Search for the same mistake elsewhere and list it, but don't fix it in this change.
After 3 ruled-out causes or 2 failed fixes, stop and report what you learned; revert
only your own unsuccessful changes, keep useful tests and diagnostics, never touch
unrelated work.
Guardrail: the regression test stays in the suite.
Report: symptom, root cause, proof, the fix, before and after output and what you could
not verify.
```

**What it covers:** the AI making the error message disappear instead of fixing the problem, by deleting the check, hiding the error or changing the test and going in circles while your code gets worse.
**Sources:** [Google SRE, effective troubleshooting](https://sre.google/sre-book/effective-troubleshooting/) · [MDN, Error.stack](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/stack)
