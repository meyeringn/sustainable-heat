# Open Questions — SustAInable

The hardest part of building an honest ML tool is knowing
where it might fail. These are the questions I haven't
fully solved yet — and that I'm actively thinking about.

---

## 1. The Reporting Lag Problem
NSSP syndromic surveillance data has a reporting lag of
7–14 days. This means the labels we train on may not
accurately reflect what happened *during* a heat event —
only what got reported afterward. How do we build a model
that is robust to this label noise without systematically
underestimating risk in fast-moving events?

## 2. The Historical Data Gap Problem
Structural vulnerability data from the ACS reflects
*current* conditions. But we're training on heat events
going back to 2010. Neighborhoods change — poverty rates
shift, housing stock turns over, demographics move. How
do we account for the fact that 2012 vulnerability
features may not accurately describe a 2012 neighborhood
the way 2024 features describe a 2024 neighborhood?

## 3. The Undercount Problem
The gap between 2,415 official heat deaths and ~11,000
estimated heat deaths is not random. Deaths are more
likely to be undercounted in communities that are
already underserved by health data infrastructure —
the same communities SustAInable is trying to prioritize.
If our labels systematically undercount outcomes in
high-vulnerability ZCTAs, the model may learn the
wrong signal. How do we correct for this?

## 4. The False Positive Fatigue Problem
If SustAInable flags 40% of ZCTAs as elevated risk
during every heat event, city OEMs will stop trusting
it within two seasons. Precision matters for adoption
even if recall is the primary metric. What is the
right precision floor that keeps the model credible
with the people who have to act on it?

## 5. The Community Challenge Question
SustAInable includes SHAP explainability so residents
and CBOs can see *why* a ZIP was flagged. But what
happens when a community disagrees with a score that
reflects historical data gaps rather than current
conditions? What is the right mechanism for community
override — and how do we build that without creating
a vector for political manipulation of resource
deployment?

---

*These questions are not blockers. They are the work.
If you have thoughts on any of them, open an issue
or reach out directly.*

**Nico Meyering** · meyeringn@gmail.com ·
[LinkedIn](https://www.linkedin.com/in/nicolasmeyering)
