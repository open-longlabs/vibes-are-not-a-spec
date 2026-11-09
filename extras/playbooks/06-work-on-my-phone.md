# Phone LARP

You say: make it work on my phone, make it responsive

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Phone LARP.
Assume it breaks on a phone until each width proves otherwise.
Propose the 3 tasks that must work; I only correct them.
Using device emulation, run them at 320, 360, 390 and 430 wide in portrait, 768 wide and
one phone in landscape, with screenshots of every step.
Emulation proves only the browser you ran; the real keyboard, browser bars, notch and
iPhone focus zoom stay UNVERIFIED without a real device.
Give me exact URLs and steps for a 2-minute check on my own phone.
Check:

(1) the viewport meta tag exists and doesn't block zooming;
(2) horizontal scrolling: at each width, compare document scrollWidth with the window
    width and name the element that overflows;
(3) tap targets measured against WCAG 2.5.8 (24 by 24 CSS px unless the spacing,
    equivalent, inline, user agent or essential exception applies, recording which) and
    44 by 44 recommended for primary actions as our own rule;
(4) inputs under 16px font size flagged as an iPhone zoom risk, to confirm on a real
    phone and never fixed by disabling zoom;
(5) forms: correct type, inputmode and autocomplete so the right keyboard and autofill
    appear;
(6) 100vh layouts cut off by the browser bars (dvh or svh handle the bars, not the
    keyboard);
(7) the on-screen keyboard covering the active input or submit button;
(8) content under the notch or home bar (safe-area-inset);
(9) anything that only works on hover;
(10) fixed headers, banners and chat bubbles covering content or buttons;
(11) tables, modals, menus and long words at 320 wide;
(12) text enlarged to 200% still readable with nothing cut off;
(13) if speed is a complaint, run the Speed LARP on mobile.

For each finding: severity, width, the screenshot or measured value that proves it, the
smallest fix and the guardrail: an automated test at each width that fails on horizontal
overflow and completes the 3 tasks.
Desktop must look the same as before unless I agree.
```

**What it covers:** the page sliding sideways, buttons too small to hit, the keyboard hiding the form, the phone zooming into fields, content stuck behind the notch.
**Sources:** [WCAG 2.2, target size minimum](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html) · [Apple HIG, accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility) · [MDN, viewport meta](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta/name/viewport) · [MDN, autocomplete](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/autocomplete) · [web.dev, viewport units](https://web.dev/blog/viewport-units) · [WCAG 2.2, resize text](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html)
