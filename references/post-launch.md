# Post-Launch Mode — Feature Triage

Use this mode when the product is live and the user asks "should I add X?", shares user feedback, debates a roadmap, or is rattled by a competitor's feature. The output is a **Feature Triage**: BUILD / DO MANUALLY / WATCH / NO — verdict first, with the evidence standard that produced it.

The default answer is **no**. A live product's scarcest resource is the builder's attention on the One Metric; every feature is a withdrawal from that account. The burden of proof is on the feature, never on the status quo.

## Method

### Step 1 — Re-anchor on the hypothesis and the One Metric

Restate the original bet and the current state of the One Metric (ask if unknown — this is the one permitted question, because triage without the metric is taste, not triage). Two very different regimes:

- **Metric not yet proven** (pre-signal): the only features worth considering are ones that remove a step between users and the core value. Everything else is procrastination with a roadmap.
- **Metric proven** (post-signal): expansion is legitimate — but each feature must now defend itself with evidence, not vibes.

### Step 2 — Grade the evidence

Score the request against the evidence ladder. Be suspicious of anything below rung 3.

| Rung | Evidence | Weight |
|---|---|---|
| 1 | Builder thinks users will want it | Zero. This is how the original bloat happened. |
| 2 | One user mentioned it once | Noise. Log it. |
| 3 | ≥5 users asked **unprompted**, in their own words | Signal. Now worth analysis. |
| 4 | Users are churning or refusing to pay, citing this gap | Strong. Likely Trust-layer debt. |
| 5 | Users are paying for a duct-tape workaround (spreadsheet, Zapier, a second tool) | Strongest. They've priced it for you. |

Two correction factors:

- **Listen to the problem, not the solution.** Users request features ("add folders!") but experience problems ("I can't find my stuff"). Triage the underlying problem; the right build may be search, not folders.
- **Weight by persona.** Five requests from the target persona outweigh fifty from tourists. A request that pulls toward a different persona is a pivot proposal in disguise — name it as such.

### Step 3 — Run the cost side

Even rung-4 evidence doesn't auto-build. Check:

- **Loop tax** — does the feature add steps, choices, or UI between new users and the core value? Features that complicate the loop need rung-5 evidence.
- **Maintenance tail** — integrations, notification systems, and anything with someone else's API keep costing after they ship. Estimate the tail, not just the build.
- **Concierge first** — can the builder deliver the outcome manually for the requesters this week? Manual delivery is the cheapest possible test of whether they actually wanted it. Most "must-have" requests die quietly when offered a manual version — which is the answer.

### Step 4 — Verdict

- **BUILD** — rung ≥4 (or rung 3 with trivial cost), serves the original persona, doesn't tax the loop. Scope it with Pre-Build discipline: the *enough* version of the feature, with its own definition of done.
- **DO MANUALLY** — real demand, automatable later. Deliver by hand, count takers, build when the hand hurts.
- **WATCH** — rung 2–3. Log it with an explicit promotion trigger ("becomes BUILD at 5 unprompted asks or first churn citing it"). A logged feature with a trigger stops nagging the builder; an unlogged one nags forever.
- **NO** — rung 1, wrong persona, competitor envy, or loop tax exceeding the evidence. Say it plainly and give the user the one-line reply to send to whoever asked: declining gracefully is part of the deliverable.

**On competitor features specifically:** a competitor shipping X is rung-1 evidence (someone *else's* builder thought users want it). Competitors are allowed to be wrong. The only competitor signal that matters is rung 4 — your users churning *to* them and saying why.

## Output template

```markdown
# Feature Triage — [feature] for [Product]

## VERDICT: [BUILD / DO MANUALLY / WATCH / NO]

**Original bet:** [hypothesis]
**One Metric now:** [state]
**Evidence rung:** [1–5] — [what the evidence actually is]
**Loop tax:** [none / describe]
**Maintenance tail:** [none / describe]

## Reasoning
[3–6 sentences. Problem behind the request, persona weighting, cost.]

## The call
[If BUILD: the enough version + definition of done. If DO MANUALLY: this week's manual play. If WATCH: the promotion trigger, verbatim. If NO: the one-line reply to send to the requester.]
```

## Worked example (condensed)

**User input:** "My CRO audit SaaS has 14 paying users. Three things: (1) a user asked for white-label PDF reports, (2) a competitor just launched a Chrome extension, (3) I think I should add team accounts because agencies might buy it."

> **White-label PDFs — DO MANUALLY.** Rung 3 borderline (1 ask, but from a paying agency — persona-weighted up). Zero loop tax. This week: take their logo, restyle the report by hand, charge ₹X extra for it, and offer the same to your other agency users. If 3+ take it, BUILD the enough version: a logo upload and a color variable. Not a template editor.
>
> **Chrome extension — NO.** Rung 1: evidence that the competitor's founder has an opinion, nothing more. None of your 14 payers has asked. Watch one number only: churn that mentions it. Reply if anyone asks: "On the list — what would you use it for day-to-day?" (which converts rung-1 into real evidence or silence).
>
> **Team accounts — WATCH, and name it honestly: this is rung 1, your own voice.** "Agencies might buy it" is the sentence that bloats every roadmap. You have 14 users and an unproven retention metric — multi-tenancy now is weeks of work taxing every future feature. Promotion trigger, verbatim: *becomes BUILD when 5 paying users ask to add a teammate, or when an agency offers to prepay for seats.* Until then, shared logins are fine and you know it.
