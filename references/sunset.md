# Sunset Mode — The Clean Kill

Use this mode when a project has hit one of the Kill Criteria its builder signed, or when a Drift Audit has routed here, or when the user says some version of "should I kill this?", "I think this is dead", or — the saddest tell — "I haven't opened the repo in a month, what do I do?". The output is a **Sunset Verdict**: KILL / REVIVE WITH NEW HYPOTHESIS / HAND OFF. Never "keep going."

The skill exists to tell builders what is enough. Enough to stop is part of that. Most builders need permission to kill more than they need help to keep building. This mode gives the permission, with a process, so the next project doesn't inherit this one's debt.

## When this mode runs

Auto-route here from:

- A Drift Audit verdict of *TIME TO SUNSET*.
- A Ship Verdict where the true blockers exceed 48 hours *and* the user has already burned through one deadline extension.
- A Pre-Build session where the hypothesis can't be stated even charitably after one clarifying question — sunset the *idea* before it becomes a project.

Run manually when the user asks. Don't run sunset on a project that hasn't been given a real shot — a Ship Verdict comes first. Sunset is for projects that *have* been in front of users (or have spent enough time pretending they would be) and didn't move the One Metric.

## Method

### Step 1 — Confirm the bet failed, not the build

Pull the signed hypothesis from the Ledger. Three failure modes; only the first one is a real Sunset:

1. **The bet was wrong.** Users had the loop, used it, didn't pay (or paid once and didn't return). The market voted. → Sunset.
2. **The bet was never tested.** The build never reached users; the loop was never walked by a stranger. → Not Sunset yet. Run Ship Verdict with the 48-hour rule, ruthlessly.
3. **The bet was right but the builder is bored.** Metric is moving; user is restless because shipping is less fun than starting. → Not Sunset. Name the boredom; route to Post-Launch mode for the next feature triage; resist the new-idea.

Sunset only applies to case 1. If it's 2 or 3, say so and stop.

### Step 2 — Read the cost

Get specific about what the project actually cost and what it produced. Numbers, not vibes.

- **Days spent** since spec (from Ledger).
- **Users reached** — how many strangers tried it, how many paid, how many returned.
- **Cash in / out** — domain renewal, hosting, paid tools, paid ads. Refund obligations.
- **Reputation surface** — is there a public landing page, a Twitter thread, a Product Hunt page, an investor expecting an update?

The cost reading is what makes the kill clean later. Builders skip it because it stings; do it for them.

### Step 3 — Choose the kill shape

Three options. Pick one — never two.

- **KILL** — take it offline, refund anyone still paying, archive the repo, write the lesson. Default option. Choose this unless one of the other two clears the bar.
- **REVIVE WITH NEW HYPOTHESIS** — the build is reusable but the hypothesis was wrong. State the new bet in one sentence; re-run Pre-Build from scratch with most of the existing code in CORE/TRUST. Only choose this if the new hypothesis is genuinely different and the user can defend it without saying "but also." If the new hypothesis is "same product, smaller niche," that's a Pre-Build cut, not a Revive.
- **HAND OFF** — sell, open-source, or transfer to a co-builder. Choose this only if there's a named recipient. "Maybe someone will buy it" is not a recipient; that's a KILL wearing a Hand Off costume.

### Step 4 — Write the kill plan

Every Sunset Verdict produces three concrete actions, in order. None of them is "think about it more."

1. **Stop the bleeding.** Pause Stripe/Razorpay subscriptions today. Email existing paying users with a refund or a 90-day wind-down. Take the landing page CTA down or replace it with "this product is winding down." Cancel paid tools tied to this project only (not your general stack).
2. **Close the loop with users.** One email, hand-written, to every paying user — apology, refund or wind-down, what they should use instead. Three sentences max. No "we've decided to focus on…" corporate exit; this is a solo builder writing to humans.
3. **Bank the lesson.** One paragraph in the Ledger and ideally a public post: *what the bet was, what the data said, what the next project should NOT inherit from this one.* This is the only output that compounds across projects.

### Step 5 — Write the lesson

The single most valuable artifact of a sunset is the lesson. Force it.

Bad lesson: *"I should validate more next time."* (Generic, useless, ignored.)
Good lesson: *"I picked a persona — 'freelancers' — that's too broad. The freelancers who replied to outreach were content writers; the ones who used the product were designers; they wanted different things. Next project: pick one of the two and commit before any code."*

The lesson is allowed to be uncomfortable. It is not allowed to be vague.

## What never gets cut from a Sunset

- **Refund obligations.** If users paid for service they haven't received, refund them. Builders skip this because it hurts; the skill must not.
- **Honesty in the wind-down.** Don't disguise the kill as a "pivot" or a "strategic pause." The landing page comes down or says the truth.
- **Data return.** If users put data in, give them an export and a deletion. The Trust layer applies after death too.
- **The public post-mortem if there were public claims.** If you tweeted "building X," you owe the tweet "wound down X, here's why." Builders who skip this carry a credibility tax into the next project.

## Output template

See `templates/sunset-verdict-template.md`.

## Worked example (condensed)

**Setup:** Ledger shows a spec signed 2026-03-14 for an analytics SaaS for newsletter writers. Today is 2026-06-14 (92 days in, deadline was 2026-04-04 — slipped twice). One Metric: 10 paying writers in 60 days. Current: 1 paying, churned after month 2. Last commit 18 days ago. Domain renewal in 3 weeks.

**Verdict-first output:**

> ## VERDICT: KILL. Clean it up by Friday.
>
> **The bet that failed:** "Newsletter writers paying $19/mo would adopt a tool that surfaces their best send time, because they currently guess." The market voted: 1 paid, churned. The bet was wrong — not the build.
>
> **What it cost:** 92 days. ~$240 in hosting + domain + Beehiiv API + paid ads. One refund owed (to the churned user — yes, even though they churned; you charged after they stopped using it).
>
> **Three actions, by Friday:**
> 1. Pause the Stripe subscription. Refund the churned user $38 (two months). Replace the landing page hero with: *"This product is winding down. Existing users keep access until 2026-09-14."*
> 2. Email the 47 free-trial users (you have their addresses): three sentences. What it was, why it didn't work, the one alternative you'd point them at instead.
> 3. Don't renew the domain. Let it expire 2026-07-05. Archive the repo as `newsletter-analytics-sunset-2026-06`.
>
> **The lesson — write this into the Ledger AND post it publicly:**
>
> *Newsletter writers say they want data about their sends. What they actually want is one specific tactic that will grow their list this week. "Best send time" was a metric framing of a problem they experience as a tactic problem. The data answer required them to integrate a tool; the tactic answer would have required nothing. Next project: ask the persona what they'd pay for THIS WEEK, not what data would help them in general. "What would you pay me to do for you this week?" is the only validation question I trust now.*
>
> **What you keep:** the audience list you built. The Beehiiv integration code. The lesson above. Everything else, including the affection for the idea, gets composted.
>
> **Definition of Done:** the domain expires, the inbox is empty of refund requests, and your next Pre-Build session opens with the lesson above already pasted at the top.

Note the shape: a verdict that's the harder of the three (KILL beats REVIVE most of the time, and REVIVE beats HAND OFF), numbers everywhere, a literal Friday deadline on the kill itself, and a lesson that's specific enough to change the next project's behavior.
