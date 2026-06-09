# Pre-Build Mode — The Enough Spec

Use this mode when the user has an idea, a spec, a PRD, or a feature list and has not started building (or has barely started). The output is an **Enough Spec**: the smallest buildable version that tests the hypothesis, with everything else explicitly cut and sequenced.

## Method

Work through these steps in order. Steps 1–3 are analysis; steps 4–6 produce the spec.

### Step 1 — Extract the hypothesis

Reduce the idea to: *[specific person] will [specific action] because [specific reason]*.

- "People" is not a person. "Founders" is barely a person. "DTC founders doing ₹20L–₹2Cr/month who run their own ads" is a person.
- The action must be costly to the user — pay, return, invite, switch. Free signup is not an action; it's a twitch.
- If the user's pitch contains two hypotheses ("it's a marketplace AND a community"), pick the one the revenue depends on and park the other in LATER. Two hypotheses means zero focus.

If no hypothesis can be extracted even charitably, stop and say so. An Enough Spec for an aimless idea is just a smaller aimless idea. Help the user find the bet before scoping it.

### Step 2 — Draw the Core Loop

Write the loop as numbered steps from "user has the problem" to "user receives the value," in the user's shoes, ignoring all internals.

Rules:

- **One persona, one entry point, one path.** If the idea has buyers and sellers, pick the side whose behavior is the riskier assumption and fake the other side manually.
- **Each step earns its place.** A step survives only if the value literally cannot be delivered without it. "Create an account" almost never survives — value first, account later (or never; an email field is an account).
- **The loop should be 3–6 steps.** Seven or more means a hidden second product is inside; find it and cut it.

### Step 3 — Bucket every feature

Take every feature — stated, implied, or buried in the user's prose — and run the five cut tests from SKILL.md. Assign each to CORE / TRUST / LATER / NEVER with a one-line reason. Do not skip features to be polite; the implied ones ("obviously it'll have user profiles") are the most dangerous because nobody decided them.

When a feature list is infrastructure-shaped (auth, admin, dashboards, notifications, settings), pull the substitute from `references/cut-patterns.md` instead of reasoning from scratch.

### Step 4 — Set the One Metric and Kill Criteria

Pick the single number that proves the hypothesis. Calibrate to stage:

| Stage of trust | Acceptable metric |
|---|---|
| Will anyone pay? | First N payments from strangers (not friends) |
| Will anyone use it twice? | N users who complete the loop in week 1 *and* week 2 |
| Will anyone switch? | N users who import/migrate real data |

Then set the kill criteria as the inverse with a deadline: *"If fewer than [N] [actions] happen within [Z] days of launch, stop or pivot."* Make N small and honest — 10 paying strangers is a real signal; 1,000 visitors is noise.

### Step 5 — Set the Ship Deadline

Estimate the CORE + TRUST build honestly, then set the deadline at that estimate — not estimate plus buffer. The deadline's job is to apply back-pressure on scope: when the build runs over, the answer is to cut, not to slip. For a solo builder, an Enough Spec that can't ship in 1–3 weeks is not an Enough Spec; return to step 3 and cut harder.

### Step 6 — Write the spec

Use the template below (also at `templates/enough-spec-template.md`). Keep the whole spec under one page. A spec the builder can hold in their head is a spec that survives contact with the build.

## Output template

```markdown
# Enough Spec — [Product Name]

**The bet:** [hypothesis in one sentence]
**Ship deadline:** [date, days from now]
**Definition of Done:** [one sentence — the observable state that means "stop building, start selling"]

## The Core Loop
1. [step]
2. [step]
3. [step]

## Build this (CORE)
- [feature] — [why the loop breaks without it]

## Build this minimally (TRUST)
- [feature] — [the walk-away it prevents] — [the minimal version, e.g. "Stripe payment link, no billing portal"]

## Cut — LATER (build when the trigger fires)
- [feature] — trigger: [observable condition, e.g. "≥5 users ask unprompted" or "after 50 paid users"]

## Cut — NEVER (for now)
- [feature] — [the test it failed, bluntly]

## The One Metric
[metric] — Kill criteria: if [threshold] doesn't happen within [days] of launch, [stop/pivot decision].

## Manual-for-now plan
[What the builder does by hand instead of building: fulfillment, support, onboarding, the other side of the marketplace.]
```

## Worked example (condensed)

**User input:** "I want to build a tool where freelancers can send clients a branded portal with proposals, contracts, invoices, file sharing, a chat, client accounts, payment processing, a dashboard with analytics, templates marketplace, and team seats later."

**Verdict-first output:**

> **The Enough version of this is a branded proposal-to-payment page. Ship in 12 days.**
>
> **The bet:** Freelance designers will pay ₹999/mo to send clients one branded link that gets proposals approved and paid faster, because chasing approvals over email is their most-hated task.
>
> **Core Loop:** (1) Freelancer pastes proposal + price → (2) gets a branded link → (3) client opens link, clicks Approve, pays → (4) freelancer gets the money and a notification.
>
> **CORE:** proposal page generator, approve button, Stripe/Razorpay payment, email notification on approval.
> **TRUST:** payment actually settles; page doesn't break on mobile (clients approve from phones); the freelancer's logo shows (it's the "branded" promise on the landing page).
> **LATER:** contracts/e-sign — trigger: 5 users ask; file sharing — trigger: same; invoicing — trigger: paid users churn citing it.
> **NEVER (for now):** client accounts (clients will not create accounts to pay you — the link IS the account); chat (email exists; failed the spreadsheet test); analytics dashboard (at <100 users, the builder can read the database; failed the concierge test); templates marketplace (a second product wearing the first one's clothes); team seats (multi-tenancy at zero users is a month of work to organize data nobody has).
>
> **One Metric:** 10 strangers paying ₹999 within 21 days of launch — or kill it.
> **Manual-for-now:** onboard the first 20 freelancers personally over WhatsApp; build their first proposal page for them.
>
> **Definition of Done:** a freelancer you've never met sends a link, their client pays through it, and you didn't touch anything.

Note the shape: verdict first, every cut has a reason, every LATER has a trigger, numbers everywhere, one page.
