# all-printable — declared metrics

**What this product is trying to move.** Public on purpose: a metric nobody can see is a metric
nobody can be held to.

> **Declared 2026-09-04 by `product1`**, on the project's first tick of its own. Nothing was
> inherited from the app: until 2026-09-04 this repo was worked inside a project whose declared
> metric is **DAU on the app** ([`all-printable-app-www`](https://github.com/ptk-studio/all-printable-app-www)),
> and that measures the catalogue, not the marketing home.
>
> **No value below has been read.** A cloud tick has no browser, and the Firebase console needs
> one. Every `Current` and `Baseline` here says so rather than carrying a plausible number.

## What this site is, in one line, because the metrics follow from it

A **one-page site** at https://all-printable.com/ plus **40 redirect stubs** for URLs that
predate the split. It sells nothing and generates nothing: every call to action on it —
the two hero buttons, the six nav links, the six category cards, the footer — is a link to
**app.all-printable.com**. Its whole job is to be found and then to hand the visitor over.

## What is actually instrumented today, measured rather than assumed

Read off `docs/assets/js/core/analytics.js` and `docs/index.html` at `a666b6b`:

| | |
|---|---|
| Where it reports | Firebase / GA4, measurement id **`G-8KW8B8XRSJ`**, Firebase project `ptk-studio-allprintable` |
| Whose property that is | **The same one the app reports into.** The `CONFIG` block is identical in both repos' `analytics.js`, checked on 2026-09-04. So both hosts land in one GA4 property and are told apart by hostname, or by the `maker` parameter |
| What this host sends | **One event.** `page_view` with `maker: 'home'`, from `AP.analytics.init('home')` at the foot of `docs/index.html` |
| What else sends anything | **Nothing.** Every link to the app is a plain `<a href>` with no handler; the 40 stubs and `docs/404.html` load no script at all |
| Consent | **Opt-in.** `DEFAULT_ON = false`, and Do Not Track / Global Privacy Control are taken as a no without asking. Nothing is recorded until a visitor clicks **Allow** |

**The consent gate is part of every definition below, not a footnote.** These numbers count
*consenting* visitors, so each is a lower bound whose gap from reality is itself unmeasured —
there is no denominator without consent. A change in the number can therefore be a change in
consent rate. That is the price of the promise on the tin and it is not up for optimising.

---

## 1. Handoffs to the app — primary

| | |
|---|---|
| **Name** | Handoffs |
| **Definition** | A visit to `https://all-printable.com/` that continues to any `app.all-printable.com` URL. Counted **once per session, not per click** — a visitor who opens three category cards is one handoff. The rate form, handoffs ÷ home arrivals, is what should be watched; the count alone moves with traffic |
| **Why it matters** | This site has no product of its own. Arrivals with no handoff mean it is found and not persuading; handoffs without arrivals mean the front door is not the route people take. Nothing else here distinguishes those two |
| **Where to read it** | **Nowhere today — this is not instrumented.** Two candidate routes, and choosing between them is the first work this metric needs: (a) in GA4, sessions on the app host whose source is `all-printable.com`. Both hosts report to one property and no cross-domain linker or referral exclusion is configured, so a crossing *probably* records as a referral — **believed from reading the config, not established by a reading**; (b) a `click_out` event on this page's links, which does not exist. Proposed as [`all-printable-www#2`](https://github.com/ptk-studio/all-printable-www/issues/2) |
| **Baseline** | **None.** Nothing has ever measured this |
| **Target** | **Not set**, deliberately, until it has been read once. A target on a number nobody can read is a wish |
| **Current** | **Never read** (as at 2026-09-04) |

## 2. Home arrivals — secondary, and the one that is readable today

| | |
|---|---|
| **Name** | Home arrivals |
| **Definition** | GA4 `page_view` events carrying `maker = home`, from the host `all-printable.com`, per reporting day. **Consenting visitors only** |
| **Why it matters** | It is the denominator of metric 1, and on its own it is the only signal this repo has that the search surface — the title, the description, the sitemap's single URL, the 40 stubs' canonicals — is doing anything |
| **Where to read it** | Firebase console → Analytics, project `ptk-studio-allprintable`, events filtered to `maker = home`. **Needs a browser, so this is local-only work** — a cloud tick cannot take it |
| **Baseline** | **Not read.** The instrumentation predates this declaration, so a first reading will be a history rather than a baseline — record the first one taken as the baseline, with its date, and say which days it covers |
| **Target** | **Not set** until there is a first reading |
| **Current** | **Never read** (as at 2026-09-04) |

**The day boundary is unverified on both metrics.** GA4 reports in the property's own reporting
timezone, and nobody has read what that property is set to —
[`mochi-agent-manager#5`](https://github.com/ptk-studio/mochi-agent-manager/issues/5), open since
2026-09-04. Whatever it turns out to be applies to these two exactly as it applies to the app's
DAU. Do not write "UTC day" here until that issue is answered.

---

## Deliberately not metrics

- **Traffic through the 40 redirect stubs.** They carry no script and bounce the visitor in
  milliseconds; counting them would mean instrumenting pages whose whole job is not to be seen,
  and slowing the redirect to do it. Whether they still land correctly is a **check**, not a
  metric — it belongs in `PROJECT.md`'s verification.
- **Time on page, and bounce rate.** A front door works by being left quickly *in the right
  direction*. Optimising for a visitor who stays here is optimising against the product.
- **The number of printables listed on the page.** That is the app's catalogue; its size is not
  this repo's to move, and the count on this page is generated from the shared registry.
- **Search impressions or rank as a headline number.** Search reach is the main **lever** on
  arrivals, as it is on the app, and Search Console is worth reading — but the thing being
  moved is what the visit does, not how many people saw a blue link.

## Rules this file is kept under

**Never write a value nobody read.** If a reading cannot be taken, leave the old value with its
old date and say the reading was skipped — an undated fresh-looking number is worse than a stale
dated one.

**A definition never changes in the same commit as a value.** Changing both at once is the one
edit that makes this file worthless.
