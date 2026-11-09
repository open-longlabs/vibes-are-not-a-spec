# Usability LARP

You say: make it easy to use, people get confused

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Usability LARP.
Assume a first-time visitor gets stuck until a walkthrough proves otherwise.
Work out the likely user and propose 3 start-to-finish tasks from the product itself; I
only correct them.
Run each task in a real browser with the right starting point (signed-out visitor, new
account, or returning account with realistic data), record every screen, click, required
field and error with screenshots and verify the result was really saved.
Check:

(1) the first screen says what this is, who it's for and what to do next;
(2) steps per task and every step that could be removed or defaulted;
(3) sign-up or payment demanded before the user sees any value;
(4) words: buttons and labels in the user's language, no internal or technical terms;
(5) forms: every field needed, visible labels rather than placeholders, correct input
    types, errors next to the field saying how to fix it, typed data kept after an
    error;
(6) feedback: every action shows that it's working and that it finished;
(7) dangerous actions need a confirmation or can be undone;
(8) dead ends: empty states, 404s and errors offer a next step;
(9) orientation: the user can tell where they are and go back and browser back works;
(10) keyboard: every task can be finished without a mouse, focus is visible, controls
    have names.

For each finding: severity, the screenshot and step that prove it, the smallest fix and
the guardrail: an end-to-end test per task, with a maximum step count written down.
Don't redesign pages or remove features without asking.
Your walkthrough is not a user test: mark "real users understand it" as UNVERIFIED and
give me a short script to watch 5 people try the 3 tasks without helping them.
```

**What it covers:** the moments people give up: not understanding the first screen, too many steps, forced sign-up, confusing forms, no sign that anything happened and dead ends.
**Sources:** [NN/g, 10 usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) · [NN/g, why you only need to test with 5 users](https://www.nngroup.com/articles/why-you-only-need-to-test-with-5-users/) · [WCAG 2.2, keyboard](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html) · [WCAG 2.2, error suggestion](https://www.w3.org/WAI/WCAG22/Understanding/error-suggestion.html)
