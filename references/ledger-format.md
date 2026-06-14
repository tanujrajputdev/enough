# The Ledger — `.enough/` Format

The Ledger is what makes `enough` longitudinal instead of one-shot. Every verdict the skill produces is written to a file inside `.enough/` at the project root. Future sessions read the Ledger before answering, so cuts get audited, deadlines get tracked, and reversal attempts get rebutted with the original reason.

Without the Ledger, the skill is an oracle the builder can ignore. With it, the skill is an advisor who remembers what was decided.

## Directory layout

```
<project-root>/
├── .enough/
│   ├── 2026-06-14-spec.md             # Enough Spec verdicts
│   ├── 2026-06-21-ship.md             # Ship Verdicts
│   ├── 2026-06-28-triage-mobile.md    # Feature Triage verdicts
│   ├── 2026-07-05-audit.md            # Drift Audit reports
│   ├── 2026-07-12-pricing.md          # Pricing Verdicts
│   └── 2026-07-19-sunset.md           # Sunset Verdicts
```

Rules:

- **File name:** `YYYY-MM-DD-<type>[-<slug>].md`. Date first so the latest sorts last lexically. Slug is optional, used when there are multiple verdicts of the same type on the same day (usually for triage).
- **No LATEST pointer.** Sort by name; the last file of each type is current.
- **Append, never overwrite.** A new verdict supersedes the previous one of the same type; it does not delete it. History is the audit trail.
- **No subdirectories.** Flat is enough.
- **Track `.enough/` in git.** The Ledger is the spec; lose it and the project is unmoored.

If the project has no git repository or no writable filesystem (skill running in a chat-only context), skip Ledger writes and tell the user once: *"No `.enough/` ledger possible here — verdicts won't persist. Paste this into your repo if you want the next session to audit drift."*

## File format

Every Ledger file is markdown with YAML frontmatter. The frontmatter is parsed by future audits; the body is for humans.

### Frontmatter — required on every file

```yaml
---
id: 2026-06-14-spec
type: spec                      # spec | ship | triage | audit | pricing | sunset
product: Branded Proposal Pages
created: 2026-06-14
deadline: 2026-06-26            # required for spec/ship; omit for triage/audit/pricing/sunset
signed_by: Vishal Choudhary     # builder's name — commitment device
signed_at: 2026-06-14
domain: b2b-saas                # b2b-saas | consumer | creator | general
supersedes: 2026-05-30-spec     # optional — id of the prior verdict this replaces
---
```

### Body — varies by type

Every type's body section is defined by its template (`templates/<type>-verdict-template.md` or `templates/enough-spec-template.md`). All bodies end with two fixed sections that the Drift Audit reads:

```markdown
## Audit log
<!-- Appended by drift audits. Do not edit manually. -->
- 2026-06-21 — Drift Audit: on track. 4 of 4 CORE shipped, 1 of 3 TRUST shipped. 5 days to deadline.
- 2026-06-28 — Drift Audit: drifting. "Admin dashboard" (cut as NEVER on 2026-06-14) appears in /src/admin. Deadline +4d.

## Definition of Done
A stranger pays ₹999 and receives their branded page without you touching anything.
```

## Per-type body schemas

### `type: spec` — Enough Spec

Body matches `templates/enough-spec-template.md`. Required machine-readable sections inside the body:

```markdown
## The bet
[hypothesis]

## The Core Loop
1. [step]
2. [step]

## CORE
- [feature] — [reason]

## TRUST
- [feature] — [minimal version]

## LATER
- [feature] — trigger: [observable condition]

## NEVER
- [feature] — [test it failed]

## The One Metric
[metric] — Kill criteria: if [threshold] not met by [date], [stop/pivot].

## Adversarial preemption
- You will, around [date], want to re-add [feature]. The rebuttal: [reason]. Evidence that would overturn this cut: [specific signal].

## Manual-for-now plan
[what gets done by hand]
```

The CORE / TRUST / LATER / NEVER lists are what Drift Audit reads to detect cuts that crept back in.

### `type: ship` — Ship Verdict

```markdown
## VERDICT
SHIP NOW | SHIP AFTER (Xh) | NOT ENOUGH YET

## Core Loop status
1. [step] — ✅ works | ⚠️ rough | ❌ broken

## True blockers
- [item] — [hrs] — [money | data | honesty | loop]

## Felt blockers (cut)
- [item] — [polish | edge case | infrastructure | settings | one-more-feature | fear in costume]

## Ship plan
[date, literal next actions]
```

### `type: triage` — Feature Triage

```markdown
## VERDICT
BUILD | DO MANUALLY | WATCH | NO

## Feature
[name]

## Evidence rung
[1–5] — [what the evidence actually is]

## Loop tax
[none | describe]

## Reasoning
[3–6 sentences]

## The call
[scoped feature | manual play | promotion trigger verbatim | one-line reply to send]
```

### `type: audit` — Drift Audit

```markdown
## VERDICT
ON TRACK | DRIFTING | TIME TO SUNSET

## Reference verdicts
- spec: 2026-06-14-spec
- ship: (none yet)

## Cut drift
- [cut feature] — [where it appeared] — [restore the cut | promote with reason]

## Deadline drift
- Original: 2026-06-26. Today: 2026-06-28. Slip: +2d. Verdict: [extend once | sunset].

## Metric drift
- One Metric: 10 paying strangers in 21 days. Current: 3 in 14d. Verdict: [on pace | behind | dead].

## Scope drift
- File count: 47 → 92 (+96%). New top-level dirs: /admin, /reports. Verdict: [acceptable | over-built].

## Velocity
- Commits last 7d: [n]. Last commit: [date]. Verdict: [moving | stalled].

## What to do this week
[1–3 specific actions, no list bloat]
```

### `type: pricing` — Pricing Verdict

```markdown
## VERDICT
[Single price ₹X | Two prices ₹X/₹Y | Raise to ₹X | Charge now]

## What you have now
[free | ₹X with N payers | three tiers | etc.]

## The cut
[which tier to kill, which to keep, what to charge]

## Reasoning
[3–5 sentences against the pricing ladder]

## What to send to existing users
[verbatim email / changelog line]
```

### `type: sunset` — Sunset Verdict

```markdown
## VERDICT
KILL | REVIVE WITH NEW HYPOTHESIS | HAND OFF

## Why this is the verdict
[the kill criteria the project failed, with numbers]

## The clean kill
- Take payments offline: [how, by when]
- Email existing users: [verbatim message]
- Archive the repo: [date]
- What to keep for next time: [1–3 specific learnings]

## What this project taught you about the next one
[one paragraph — the lesson that should outlive the project]
```

## How the skill uses the Ledger

When the skill runs in a project with a `.enough/` directory:

1. **Read the latest `spec` file** before any verdict. This is the canonical hypothesis, cuts, and deadline.
2. **Read the latest `audit` file** if present. Don't repeat findings already addressed.
3. **Read all prior `triage` files** before any new triage — many "should I add X?" questions are the same X asked twice.
4. **Write the new verdict** to a new dated file. Set `supersedes:` if it replaces the prior verdict of the same type.
5. **Never delete files.** The audit trail is load-bearing.

When the skill runs without a `.enough/` directory but the project is a git repo, *offer to create one* with the first verdict — but ship the verdict first, don't gate on filesystem ceremony.

## The commitment mechanic

The `signed_by` and `signed_at` fields are not legal; they're behavioral. When a builder tries to reverse a cut in a future session, the skill quotes:

> *On 2026-06-14, you signed off on cutting "team accounts" because: "agencies might buy it" is the sentence that bloats every roadmap. You signed it as Vishal Choudhary. What evidence has changed?*

This works because builders rarely lie to their own past selves once the past self has a name attached. The skill never enforces the commitment — it only shows it.
