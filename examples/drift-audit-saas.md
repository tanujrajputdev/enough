# Example — Drift Audit Mode (the project that shipped, then drifted)

**Setup:**

The newsletter analytics tool from `examples/mid-build-saas.md` got a Ship Verdict on 2026-04-10 (SHIP AFTER 9 hours). The builder signed an Enough Spec the same day with a kill criterion: *"10 paying writers within 30 days of launch, or sunset."* Today is 2026-05-22 — 42 days in, 12 days past the kill window.

The builder opens a new Claude session and types:

> "Hey, can you check in on the newsletter analytics project? I shipped it like a month ago. Two paying users so far but I've been adding a few things — built the Beehiiv API integration last week and started on a comparison view for power users. Feels like momentum is back. What should I focus on this week?"

The skill detects: (a) `.enough/` exists with a `spec` from 2026-04-10 and a `ship` from 2026-04-15, (b) kill window has passed, (c) user is mid-mode without acknowledging it. Run Drift Audit.

**Enough output:**

---

# Drift Audit — Newsletter Analytics Tool

## VERDICT: DRIFTING — and honestly, you're one week from TIME TO SUNSET. The momentum you feel is the same momentum that built the wrong thing.

**Spec signed:** 2026-04-10, by [you]
**Deadline:** 2026-04-24 (ship) → met on 2026-04-15. Good.
**Days since launch:** 37
**Kill window:** 2026-05-10 (30 days post-launch). Passed 12 days ago.

## Cut drift (2 — both serious)

- **Beehiiv API integration** — appears at `/src/integrations/beehiiv/`. You cut this as LATER on 2026-04-10 with the trigger: *"5 paying users ask for the API connection unprompted."* You have 2 paying users. Neither has asked, on the record. **Restore the cut.** Move the directory to a `wip-beehiiv-api` branch you don't merge.
- **Comparison view for power users** — appears at `/src/compare/`, 3 commits last week. You cut this as LATER on 2026-04-10 with the trigger: *"unclear it's a real need — most indie writers run one newsletter."* You have 2 paying users running 1 newsletter each. **Restore the cut.** This is the LATER list defending itself; the trigger hasn't fired.

Both cuts failed for the same reason, and naming it is the work: when the One Metric stalls, builders unconsciously route around the metric and into features. Building feels like progress; selling feels like exposure. You picked the feeling.

## Deadline drift

- Ship deadline (2026-04-24): met. Don't lose this in the alarm — shipping in 9 hours when you'd been blocked for six weeks was real.
- Kill window deadline (2026-05-10): missed by 12 days. The One Metric hasn't moved since launch + 1 week.

## Metric drift

- **One Metric:** 10 paying writers in 30 days post-launch.
- **Current:** 2 paying writers, both within the first 5 days, none since.
- **Verdict: dead per the kill criterion you signed.**

Two paying strangers in the first week is real signal that *something* worked. Zero in the next 30 days is real signal that the something doesn't compound on its own — at the audience size and channel you launched into. The product isn't broken; the distribution + offer combination is.

## Velocity drift

- 14 commits in the last 7 days. Last commit yesterday.
- You are moving. You are moving on the wrong things. This is the most dangerous shape of drift the skill sees: the builder is busy enough to feel productive and far enough from the metric to feel safe.

## Scope drift

- Files: 38 (at ship) → 71 (now). +87%.
- New dirs since spec: `/src/integrations/beehiiv`, `/src/compare`. Both cut features.
- New deps: `@beehiiv/sdk`, `recharts` (already had charts; this is a second chart library for the comparison view). Compounding cost.

## What "the momentum is back" actually means

You have built two features that you cut. You have not talked to a new newsletter writer in 18 days. The momentum is engineering momentum, not market momentum. They feel the same from inside the build; they look very different from the Ledger.

## The one move this week

Not three. One.

**Delete (or branch away) `/src/integrations/beehiiv` and `/src/compare`. Then DM 30 indie newsletter writers individually with a one-line message and a Loom of one of the two paying users' actual dashboards (with permission).** No new features this week. No "let me first wire up X." If 30 hand-DM'd writers in the persona don't produce a third paying user within 7 days, run Sunset next session — the project will have given you 50 days of evidence that the bet is wrong, not the build.

If 3+ pay: rerun Pre-Build on what the new ones say in their own words. The hypothesis may need to narrow from "indie newsletter writers" to a specific kind.

## What you keep
- Two paying users — they're real. Email them this week with one question: *"What were you doing the moment you decided to pay?"* Their answer is the headline of the next landing page.
- The 9-hour ship was a real cut. Keep that pace as the baseline; don't accept the next "two weeks from done" without quoting yourself this audit.

## Definition of Done (unchanged from spec)
A writer you've never spoken to uploads their export, sees their best send time, and pays — while you're asleep.

## Audit log entry written to `.enough/2026-05-22-audit.md`
> 2026-05-22 — Drift Audit: DRIFTING. Cut features back in code (`/src/integrations/beehiiv`, `/src/compare`). Metric dead per kill criterion (2 paying / 10 target, +12d past window). Velocity high on wrong work (14 commits / 7d, 0 new users contacted / 18d). Verdict: one week to TIME TO SUNSET unless 30-DM play produces 3+ new payers.

---

**Note the moves:** the audit refuses to congratulate the user on building cut features (which the user clearly came in hoping to hear); names "the momentum is back" as the specific cognitive trap it is; quotes the signed spec back verbatim instead of relitigating; gives exactly one move and pre-announces the Sunset trigger so next session isn't a surprise; preserves the two real wins (shipped fast, two real payers) so the verdict is honest, not punitive.
