# Design LARP

You say: make it look professional, make it look better, make it clean

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Design LARP.
Assume it looks unfinished until screenshots prove otherwise.
Before judging, ask me: who is this for, 3 sites I like and 1 I don't and why.
If I have none, propose 2 written directions and wait for my choice.
Capture screenshots of the 3 main pages at 1440 and 390 wide, plus empty, loading, error
and success states.
Then check:

(1) type: list every font family, size and weight in use; flag more than 2 families or
    sizes with no clear scale for review, FAIL only on a violated requirement or
    demonstrated usability defect; and, as our own readability recommendation rather
    than a failure, body text under 16px or lines over about 80 characters;
(2) spacing: list every margin, padding and gap value; flag near-duplicates like 13, 14
    and 15px for review and keep intentional adjustments;
(3) hierarchy: each page has one h1 and one visually dominant primary action;
(4) colour: list every colour; text contrast at least 4.5:1, large text at least 3:1 and
    3:1 for the visual parts needed to identify a control;
(5) consistency: count the variants of buttons, inputs, cards, corner radius and shadows
    and name every variant with no purpose;
(6) alignment: elements off the shared grid or with uneven edges;
(7) states: hover, keyboard focus, disabled, empty, loading, error and success exist for
    every interactive element;
(8) leftovers: lorem ipsum, placeholder or broken images, default favicon, default page
    titles, mixed capitalisation, emoji used as icons;
(9) trust: real contact, privacy and legal links that work.

For each finding: severity (P0/P1/P2), the screenshot or file:line that proves it, the
fix and the guardrail that stops it coming back.
Reuse the existing design system; consolidate only the values behind a demonstrated
defect and keep intentional exceptions.
Don't rewrite copy, change the brand or invent logos, testimonials or numbers.
Guardrail: a check that fails on colours or spacing values outside the tokens, plus
before and after screenshots at both widths.
```

**What it covers:** the reasons a site looks homemade: too many fonts and sizes, random spacing, nothing that leads the eye, five kinds of button, placeholder leftovers, missing states.
**Sources:** [WCAG 2.2, contrast minimum](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) · [WCAG 2.2, non-text contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html) · [WCAG 2.2, visual presentation](https://www.w3.org/WAI/WCAG22/Understanding/visual-presentation.html) · [NN/g, usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)
**Our choice, not a standard:** at most 2 font families, the spacing rule.
