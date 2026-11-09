# Speed LARP

You say: make it fast, make it efficient, it is slow, get 100 on Lighthouse

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Speed LARP.
Assume every "it's fast" is a guess until a measurement says so.
Pick up to 3 page types that matter (include a logged-in page if the app has one) and
confirm each URL renders its real content, not a redirect or error.
Fixed, written-down setup: production build, Lighthouse version, mobile emulation, same
throttling, cold cache; 3 runs per page, keep all, report medians for score, LCP, CLS,
TBT, transferred KB and requests; add PageSpeed Insights field data if it exists, with
its period, mobile or desktop and URL or whole origin, judged at the 75th percentile and
kept separate from lab medians (none is "unknown", not "good").
Targets: LCP 2.5 s or less, INP 200 ms or less, CLS 0.1 or less, TBT under 200 ms,
Lighthouse performance 90 or more; 100 is not required.
Then find the cause in the trace, not in a checklist:

(1) the LCP element (image, poster or text) and which part is slow: server response,
    late discovery, download or render;
(2) CSS, fonts and scripts blocking first paint or LCP;
(3) the largest transfers and whether the first screen needs them;
(4) main-thread tasks over 50 ms during load and what runs in them;
(5) real interactions (menu, dialog, typing, checkout in test mode) measured in the
    DevTools performance panel, because TBT is not INP;
(6) the insertion, image, font or banner causing each layout shift, including after
    load;
(7) caching and compression on HTML, JS, CSS and media and what a repeat visit downloads
    again;
(8) every third-party script with its size, main-thread cost and load timing;
(9) slow server responses and requests that run one after another but could run
    together.

Fix only what a trace points at, one change at a time, using what the framework already
offers; never remove consent, analytics, auth or checkout and never change the design
without my yes; HTML may be cached with revalidation, personal pages never shared.
After each change, same setup, 3 runs, compare the raw metric against the run-to-run
spread, keep it or revert.
Guardrail: the named interactions still work after deferred scripts load, before/after
screenshots at mobile and desktop match, accessibility, best practices and SEO don't
drop.
Log per change: finding, change, before, after.
```

**What it covers:** why a page is slow on a phone, measured: the biggest thing on screen loading late (LCP), the page jumping (CLS), taps reacting slowly (INP), heavy files, missing caching, third-party scripts. And the honest target: Lighthouse calls 90 to 100 good.
**Sources:** web.dev: [Web Vitals](https://web.dev/articles/vitals), [Optimize LCP](https://web.dev/articles/optimize-lcp), [INP](https://web.dev/articles/inp), [CLS](https://web.dev/articles/cls), [HTTP cache](https://web.dev/articles/http-cache) · Chrome: [Lighthouse performance scoring](https://developer.chrome.com/docs/lighthouse/performance/performance-scoring), [TBT](https://developer.chrome.com/docs/lighthouse/performance/lighthouse-total-blocking-time)
