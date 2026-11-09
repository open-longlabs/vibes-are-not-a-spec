# AI Quality LARP

You say: make it smarter, the AI gives bad answers

Paste this together with the [rules](00-rules.md) into your coding agent.

```
AI Quality LARP.
Assume every "it got smarter" is one lucky answer until a test set says otherwise.
Ask me: smarter at what and what does a good answer look like?
Collect 20 to 50 real examples with the expected result, including hard cases, missing
information and cases where the right answer is "I don't know" or "ask a person".
Tune on those.
Afterwards have me or a separate process supply unseen cases; never call examples you
have already read a blind test.
Write down how each answer is scored.
Run the current version and record the baseline, cost and response time.
Then sort every failure:

(1) wrong facts or invented details;
(2) it never received the data it needed;
(3) retrieval returned the wrong document or none;
(4) instructions missing, contradictory or buried;
(5) no examples of good output;
(6) output format broken;
(7) wrong tool, wrong arguments or a tool result ignored;
(8) answered when it should have refused or asked;
(9) forgot earlier context or lost it to truncation;
(10) too slow or too expensive.

Fix the largest failure group first, one change at a time, usually starting with data,
retrieval and instructions and changing the model last (our practice, not a law).
Keep a change only if the working set improves and nothing important gets worse.
For each finding: severity, the example IDs and the real outputs that prove it, the
change, before and after scores and the guardrail: the test set runs before every
prompt, model or data change.
Report the score on the unseen cases once, at the end.
Don't add autonomy, new tools or a bigger model to chase the score without asking me.
A handful of examples is directional, so say how many cases the result rests on.
```

**What it covers:** finding out why the AI in your product gets things wrong. It might not have the right data, your instructions might contradict each other, or it answers when it should ask.
**Sources:** [OpenAI, evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) · [Anthropic, building effective agents](https://www.anthropic.com/engineering/building-effective-agents) · [Anthropic, demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
