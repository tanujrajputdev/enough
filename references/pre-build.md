# Pre-Build Mode — The Enough Spec

Use this mode when the user has an idea, a spec, a PRD, or a feature list and has not started building (or has barely started). The output is an **Enough Spec**: the smallest buildable version that tests the hypothesis, with everything else explicitly cut and sequenced.

## Before you start

Two preflight checks:

1. **Check for a prior Ledger** at `.enough/`. If a prior spec exists for this product (or for a different product whose deadline is unresolved), name it and either supersede with intent or route to Sunset on the old one before starting a new spec. The skill never produces a Pre-Build that quietly ignores an unresolved Ledger.
2. **Dispatch the domain pack.** Detect B2B SaaS / Consumer / Creator / general from the brief and read the matching `references/domains/<domain>.md` before cutting. The cut tests below are recalibrated by the pack.

## Method

Work through these steps in order. Steps 1–3 are analysis; steps 4–7 produce the spec.

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

### Step 6 — Write adversarial preemption

Before handing the spec over, name the three cuts the builder is most likely to try to reverse in the next 7–21 days. For each:

- The specific feature they'll try to re-add
- The week it'll happen, predicted from the project's shape
- The rebuttal — the exact reason from the cut, restated
- The evidence that would legitimately overturn the cut (a number, not a vibe)

Common targets for adversarial preemption: auth/accounts (week 1), the rewrite or framework migration (week 2), a notifications/onboarding flow (week 2–3), a "small" mobile companion (week 3+). Pick from the spec's actual NEVER and LATER lists.

This section is what survives the moment the builder is alone with their build at 11 pm and "thinks they need" the cut feature. It is the most-read section of the spec after launch.

### Step 7 — Write the spec

Use `templates/enough-spec-template.md`. Keep the whole spec under one page. A spec the builder can hold in their head is a spec that survives contact with the build.

Two non-negotiable fields in the template:

- **`signed_by`** — the builder's name. Ask once if unknown. The signature is a behavioral mechanism, not a legal one; future Drift Audits quote it back when cuts are reversed.
- **The Adversarial preemption section** — never empty. A spec without preemption holds for about ten days; a spec with it holds until reality changes.

## Output

Write the verdict to the conversation using the template, AND to `.enough/YYYY-MM-DD-spec.md` if a Ledger is possible. See `references/ledger-format.md` for the file's frontmatter and the audit-log section.

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
