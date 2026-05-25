# Community Engagement Framework — SustAInable

Most civic tech fails not because the technology
doesn't work — but because it was built for
communities instead of with them.

This document describes how SustAInable is designed
to involve the communities it serves at every stage:
not just as end users who receive a product, but as
co-designers who shape what the product does and
how it behaves.

---

## The Problem With "For" Without "With"

A heat risk prediction tool built without community
input will reflect the biases already present in
the data it learns from. If historically underserved
neighborhoods have been undercounted in health
surveillance data, the model will learn that those
neighborhoods are lower-risk than they actually are
— and deploy fewer resources there.

SHAP explainability (a feature built into
SustAInable's design from day one) allows communities
to see *why* a ZIP code received a particular score.
But that's only useful if communities have the
capacity, access, and trust to engage with those
explanations — and the power to do something
about scores they believe are wrong.

Community engagement is not an add-on to SustAInable.
It is a design requirement.

---

## Who Needs to Be at the Table

SustAInable is designed to serve:

- **Disabled residents** — who face 5x relative risk
of heat illness and are most likely to be missed
by conventional outreach
- **Elderly residents** — particularly those living
alone, on fixed incomes, or in housing without
reliable AC
- **Low-income renters** — in pre-1980 housing stock
with poor insulation and no legal recourse to
demand upgrades
- **Chronically ill residents** — whose conditions
make them physiologically vulnerable to temperature
extremes

These are not abstract user personas. They are my
neighbors. They are my community.

For SustAInable to work as designed, representatives
from each of these communities need to be involved
in:

1. Validating whether the model's risk tiers match
lived experience
2. Identifying neighborhoods the model may be
systematically underflagging
3. Designing the community-facing output — the plain
language risk summaries that CBOs will share
with residents
4. Establishing the community challenge process —
the mechanism for contesting a score

---

## Phase-by-Phase Engagement Plan

### Phase 2 — Data Assembly (Current)
**Who:** Disability service organizations,
public health CBOs, community health workers

**How:** Structured listening sessions asking:
- What do you already know about which neighborhoods
struggle most in heat events?
- What data do you collect that isn't in any
federal dataset?
- What would a useful alert look like for the
people you serve?

**Output:** Community knowledge layer that supplements
and stress-tests the quantitative feature schema

---

### Phase 3 — Model Development
**Who:** Same CBOs, plus residents willing to
review outputs

**How:** Present draft predictions from early model
runs and ask:
- Does this match what you saw last summer?
- Which neighborhoods feel wrong to you and why?
- What would a false negative cost your community?

**Output:** Community-validated threshold calibration
— what precision/recall tradeoff feels acceptable
to the people most affected by the errors

---

### Phase 4 — Pilot Deployment
**Who:** Pilot city partner's disability community,
elderly services network, and CBOs serving
affected ZIP codes

**How:**
- Pre-season: briefing on how the model works and
what the predictions mean
- During season: real-time feedback on whether
predictions match observed conditions
- Post-season: structured debrief on what the model
got right, what it missed, and what it should
do differently

**Output:** Pilot evaluation report published openly,
including community feedback — not just model metrics

---

### Phase 5 — Scale
**Who:** Each new city's disability and community
health ecosystem

**How:** Replication guide includes a community
engagement toolkit — not just technical
documentation. Every new deployment requires a
community engagement plan before going operational.

---

## The Community Challenge Mechanism

SustAInable will include a formal process for
communities to contest risk scores they believe
are wrong.

A CBO or community member who believes a ZIP code
has been underflagged can submit a challenge that
triggers:

1. Review of the SHAP feature contributions for
that ZIP — which factors drove the score?
2. Cross-reference with community-held knowledge
— what does the CBO know that the data doesn't?
3. Documented decision — either the score is
adjusted with explanation, or the reason for
maintaining it is published transparently

This is not a vulnerability. It is the point.
A model that cannot be challenged by the community
it affects is not a civic tech tool.
It is surveillance infrastructure with better branding.

---

## A Note on Lived Experience as Design Input

I am a Disabled person. My wife is chronically ill
with acquired disabilities including autonomic
dysfunction. Heat is not a policy abstraction
for us.

That lived experience is not a credential I list
to signal virtue. It is a design input. It shapes
which questions I ask of the data, which errors
I find unacceptable, and which communities I
am accountable to when this tool is wrong.

Every civic tech tool should be able to answer:
*Who built this, and who do they answer to?*

SustAInable's answer is: a Disabled Philadelphian
who is accountable to his neighbors.

---

**Nico Meyering, MPA**
nicmeyering@gmail.com ·
[LinkedIn](https://www.linkedin.com/in/nicolasmeyering)

*Chairman, Philadelphia Mayor's Commission on
People with Disabilities*
*VP of Growth & Partnerships, Net Impact Philadelphia*
*Equitech Futures Civic Tech Institute, CTI 2026*
