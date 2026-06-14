# Example — Mid-Build Mode (the project that's been "almost done" for six weeks)

**User input:**

> "Been building a newsletter analytics tool for indie writers for about 3 months — connects to Substack/Beehiiv exports, shows open-rate trends, best send times, subscriber-growth charts. Honestly it's been 'two weeks from done' for like six weeks. Working: CSV import, the three main charts, auth. Remaining: Beehiiv API integration (CSV works but API would be smoother), email reports, comparison view between newsletters, fixing chart colors, writing tests, the pricing page, and I want to rework the import flow because it feels clunky. Is this ready or am I crazy?"

**Setup note:** the project has no prior `.enough/` ledger (this is its first encounter with the skill). The skill detects the six-week stall as a likely drift signal, but since there's no spec to compare against, it produces a Ship Verdict directly and offers to retroactively write a spec to ground future audits.

**Enough output:**

---

# Ship Verdict — [Newsletter Analytics Tool]

## VERDICT: SHIP AFTER — 9 hours. You've been done for six weeks; the list grew to protect you from launching.

**Core Loop status: 3 of 3 working.**
1. Writer exports CSV from Substack/Beehiiv — ✅ (their side)
2. Imports it — ✅ works ("clunky" ≠ broken; see below)
3. Sees trends, best send times, growth — ✅ the three charts exist

The product you described — *upload your export, see what's working* — exists right now on your machine. Everything on your remaining list is for a product with users, and you have zero, which is the actual emergency.

## True blockers (9 hrs)
- **Pricing page + payment link — 4 hrs** — money: there is currently no way for a convinced stranger to pay you. One price, one Lemon Squeezy link, no plan matrix.
- **Import failure message — 3 hrs** — honesty/happy-path: a malformed CSV currently fails silently. The user must see "this column is missing, here's a sample file." Not a redesign — an error message and a sample file.
- **Data deletion path — 2 hrs** — data: you're storing strangers' subscriber data; "email me and I delete your data within 24h" written on the page, plus a tested manual delete query. The legal floor for holding other people's audience data.

## Felt blockers (cut from the launch path)
- **Beehiiv API integration** — one-more-feature: CSV completes the loop. Trigger: 5 paying users ask for the API connection unprompted. (Pattern: integrations earn rung-4 evidence first.)
- **Email reports** — one-more-feature: this is feature #2 of a product that hasn't sold feature #1.
- **Comparison view** — edge case: how many indie writers run multiple newsletters? A minority of a market you haven't met yet.
- **Chart colors** — polish: nobody has ever churned over chart colors who wasn't leaving anyway.
- **Tests** — infrastructure: write them for the import parser *after* real users send you real cursed CSVs to test against. Their files are better test cases than your imagination.
- **Import flow rework** — fear in costume, and the tell is in your own wording: it "feels" clunky. Six weeks of feelings, zero user reports. Ship it clunky; if 3 of your first 10 users stumble in the same place, you'll know exactly what to fix instead of guessing.

## Ship plan
**This Friday.** Tonight + tomorrow: the 9 hours above. Thursday: record a 45-second screen capture — export from Substack, drag in, charts appear. Friday: post it where indie writers already are — the Substack writers' communities, the Beehiiv Facebook group, your X — with the capture and the payment link. Personally email 10 newsletter writers you actually read and offer to run their export for them (concierge onboarding = your first user interviews).

## Definition of Done
A writer you've never spoken to uploads their export, sees their best send time, and pays — while you're asleep.

---

## After the verdict — retroactive Ledger write

Because there's no prior spec, the skill offers to write one now alongside the Ship Verdict:

> *Before you ship Friday: I'll write `.enough/<today>-spec.md` and `.enough/<today>-ship.md`. The spec captures the hypothesis you've been building toward but never wrote down, plus the kill criterion you'd otherwise skip — "10 paying writers within 30 days of launch, or sunset." Both files get signed under your name. Next time you come back to this project, the Drift Audit will check whether `/src/integrations/beehiiv`, `/src/compare`, and email-report code stayed out — and if the metric moved.*

The retroactive spec is what makes the next session's Drift Audit possible (see `examples/drift-audit-saas.md` for that session).

---

**Note the moves:** the verdict names the six-week pattern instead of politely ignoring it; "clunky" is reclassified from blocker to feeling; every cut gets a trigger so it's deferred, not dismissed; the ship plan is literal enough to execute without thinking; the Ledger write isn't gated on a perfect spec — the skill offers to bank what's known now so future audits have something to measure against.
