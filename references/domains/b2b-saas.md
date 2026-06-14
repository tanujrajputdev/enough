# Domain Pack — B2B SaaS

Apply this pack when the persona is a business buyer (a team, an agency, an ops lead, a founder buying for their company) and the One Metric is recurring revenue. Detect from the brief: phrases like "for teams," "for agencies," "for ops," "B2B," "MRR," "seats," "workspaces," "for [job title]."

The B2B SaaS overbuild instinct is *enterprise theater* — building like the product needs to convince a procurement committee before it has convinced one operator. Cut accordingly.

## The persona truths that change cuts

- **The buyer ≠ the user (sometimes).** Verify which one is the target before cutting. Builder bias is to design for the user; revenue comes from the buyer. If they're different, the bet is who reaches for the credit card.
- **Adoption is a person, not a company.** "We use it across the team" almost always means "one person convinced everyone else." Find that person; build for them.
- **Procurement is a stage, not a feature.** SSO, SOC2, MSAs, security questionnaires — these are gating features at the *deal stage*, not at validation. Pre-PMF, they are LATER with a real trigger: "deal worth ≥$24K ARR blocked on it, in writing."

## Cut tests, recalibrated for B2B SaaS

These override `SKILL.md` defaults where they conflict.

1. **Loop test — for the buyer's *outcome*, not their stakeholder report.** The loop ends when the buyer can say "yes, this saves us time/money," not when the buyer can show their boss a dashboard. If the loop's final step is a chart, suspect ego.
2. **Walk-away test — anchored to the alternative.** B2B buyers always have an alternative (a spreadsheet, an existing tool, a person doing it manually). Test walk-away as: *would they pay you in addition to keeping the alternative, or in place of it?* "In addition" is a hobby line item; "in place of" is a real business.
3. **Concierge test — extra weight.** B2B users tolerate manual fulfillment far longer than consumer users. The first 20 paying customers can be onboarded over a 30-min Zoom each; the builder learns more per call than from any analytics dashboard. Don't automate onboarding before customer 30.
4. **Multi-tenancy bias check.** Cut-patterns #7 (multi-tenancy) applies with extra force here. The B2B builder almost always wants workspaces/teams/roles by reflex. The cut: single-user login, the team shares it. Trigger to add real multi-tenancy: 5 paying *companies* (not users) request a teammate.

## Overbuild patterns specific to B2B SaaS

In addition to the general `cut-patterns.md`, watch for these:

### SSO / SAML / SCIM before the deal asks
- **Why it appears:** "Enterprise will want it." Enterprise doesn't exist yet.
- **Fails:** evidence ladder.
- **Ship instead:** email + password, hosted via Clerk/Supabase. Trigger: an enterprise deal naming a specific IDP, in writing.

### SOC2 / ISO / HIPAA prep before the first paying customer
- **Why:** "We need to be enterprise-ready."
- **Fails:** concierge test; pre-PMF compliance is a six-month detour from product.
- **Ship instead:** a public security page stating what the product does and doesn't do; a real privacy policy; encryption at rest via the hosted DB defaults. Trigger to start SOC2: a $30K+ ARR deal blocked on it.

### Custom roles & permissions
- **Why:** B2B fantasy ("admins, members, viewers, billing-only").
- **Fails:** loop test; every role multiplies test surface.
- **Ship instead:** everyone in a workspace can do everything. Trigger: a paying customer's billing person has been accidentally CC'd on something sensitive and writes in to complain.

### Audit logs as a launch feature
- **Why:** demo'ing well to "the security team."
- **Fails:** ego test pre-PMF; nobody reads them.
- **Ship instead:** a CSV export of the activity table, sent on email request. Trigger: a deal blocks on auditability with a named compliance reason.

### Account management UI (cancel/upgrade/downgrade self-serve)
- **Why:** B2B founders learn from Stripe Atlas blog posts.
- **Fails:** concierge test < 100 customers.
- **Ship instead:** "Email us to cancel or upgrade." You will reply within an hour. The reply rate is a leading retention signal you'd otherwise miss.

### Annual contracts before retention is known
- **Why:** "Annual locks them in."
- **Fails:** the pricing truth that annual is for proven retention (see `references/pricing.md`).
- **Ship instead:** monthly billing only. Trigger to offer annual: cohort retention ≥60% at month 3.

### Vertical-specific compliance ("we'll do healthcare too!")
- **Why:** TAM theater.
- **Fails:** the hypothesis names one persona; adding a vertical multiplies every compliance, legal, and feature debt forever.
- **Ship instead:** one vertical, named. Other verticals are LATER with a paying-prospect trigger.

## The One Metric for B2B SaaS

Pre-PMF: *N paying companies who renew the second month*, where N is small (3–10). Not MRR, not signups. Renewal — month-2 cash from people you didn't beg — is the only B2B signal that isn't noise.

Kill Criteria default: *if fewer than 5 companies are still paying you after 90 days, the hypothesis is wrong, not the build.*

## The Trust layer is larger here

Pre-PMF B2B users tolerate ugly UI but not data loss, mis-billing, or invoice errors. Trust includes:

- Real invoices with the customer's legal name (not "Buyer of $99 thing")
- A clear data export path — users put their team's data in; they get to take it out
- An offboarding promise — what happens to their data when they cancel, named on the page
- A working refund path — even if the page says "no refunds," there is a human who refunds when it's right to

If any of these is missing, fix it before any LATER feature.

## What an Enough Spec looks like in this domain

A B2B SaaS Enough Spec almost always reads:

- **CORE:** the one workflow that replaces the spreadsheet/manual-process the persona uses today.
- **TRUST:** payment, invoice with legal name, data export, single-user login.
- **LATER:** SSO, multi-tenancy, audit logs, billing portal, annual pricing, integrations beyond CSV.
- **NEVER (for now):** SOC2, vertical expansion, free tier, lifetime deals, custom roles.

If the user's spec has SSO, audit logs, custom roles, and SOC2 in CORE — that's the deepest cut this skill makes for them. Make it gently and directly.
