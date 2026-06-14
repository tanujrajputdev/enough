# enough

**A Claude skill that tells you when to stop — and remembers what it told you.**

Most products don't die because the builder lacked skill. They die because the builder couldn't answer one question: *what is enough?* Enough to ship. Enough to learn. Enough to stop adding features and start finding users.

`enough` turns Claude into a ruthless scope killer. Feed it an idea, a half-built project, a feature request, a pricing page, or a project you haven't opened in three weeks — it returns a verdict, not a discussion. In v2, it also remembers: every verdict writes to a `.enough/` ledger inside your repo, and future sessions audit whether the cuts held.

## What it does

The skill operates in six modes and auto-detects which one you're in:

| You say | Mode | You get |
|---|---|---|
| "I want to build X" / paste a PRD | **Pre-Build** | An **Enough Spec** — the smallest version that tests your core hypothesis, every cut explained, every deferred feature given a trigger, and the cuts you'll most likely try to reverse already rebutted in advance |
| "Is this ready to ship?" / "almost done, what's left?" | **Mid-Build** | A **Ship Verdict** — SHIP NOW, or SHIP AFTER an hour-estimated list of true blockers (max 48 hours of work, by rule) |
| "Should I add this feature?" / "users are asking for X" | **Post-Launch** | A **Feature Triage** — BUILD / DO MANUALLY / WATCH / NO, graded against an evidence ladder |
| "How's the project doing?" / new session on a project with a Ledger / deadline near or past | **Drift Audit** | A drift report — ON TRACK / DRIFTING / TIME TO SUNSET — naming the cuts that crept back in, the slip on the deadline, the gap against the kill criterion, and the one move for next week |
| "Should I kill this?" / metric dead per signed kill criteria / haven't opened the repo in a month | **Sunset** | A **Sunset Verdict** — KILL / REVIVE WITH NEW HYPOTHESIS / HAND OFF, plus the three-action kill plan and the lesson the next project should inherit |
| "What should I charge?" / "is this too expensive?" / three-tier pricing page with a question mark | **Pricing** | A **Pricing Verdict** — one specific price (or one specific change), with the floor / ceiling math, the verbatim migration email, and the page copy |

Every output ends with a one-sentence **Definition of Done** — the observable state that means "stop building, start selling."

## The Ledger — what v2 added

When the project has a writable filesystem, every verdict the skill produces is written to `.enough/<date>-<type>.md` inside the repo. Future sessions read the Ledger before answering:

- Pre-Build won't quietly start a new spec while a prior spec is unresolved.
- Mid-Build measures readiness against the *signed* Core Loop, not the loop you remember.
- Post-Launch reads prior triage so the same "should I add X?" doesn't get re-litigated.
- **Drift Audit** is what the Ledger unlocks: compare today's repo (git history, file tree, scope) against the cuts you signed off on. Cuts that snuck back get named, with file paths.
- Reversal attempts get quoted back: *"On 2026-06-14, you signed off on cutting `team accounts` because: 'agencies might buy it' is the sentence that bloats every roadmap. What evidence has changed?"*

Track `.enough/` in git. The Ledger is the spec; lose it and the project is unmoored.

## The opinions baked in

This skill is not neutral. It believes:

- **Enough = the smallest version that generates real evidence about the core hypothesis.** Not the smallest version that's impressive.
- Every feature must survive five cut tests: the loop test, the walk-away test, the ego test, the concierge test, and the spreadsheet test.
- "Builders asking *is it ready?* are almost never blocked by missing features. They're blocked by fear wearing a feature costume."
- The default answer to a new feature is **no**. The burden of proof is on the feature, never on the status quo.
- One price beats three tiers, pre-PMF. Free tiers are a tax on paid users. Annual pricing is for proven retention.
- Sunsetting a project is a verdict the skill produces; "keep going" on a dead project is not an option.
- A cut you don't *write down with a reason* is a cut you'll reverse. Adversarial preemption — naming the cuts you'll try to undo, in advance — is shipped with every spec.
- But "enough" is never a license to ship broken: payment integrity, data integrity, honesty, the legal floor, and core-path accessibility are uncuttable.

It ships with 18 general **cut patterns** and three **domain packs** (B2B SaaS, Consumer, Creator) that override the cut tests for the persona type — because cutting SOC2 from a B2B spec, "engagement" from a consumer app, or a custom LMS from a creator product all look different.

## Install

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/tanujrajputdev/enough.git ~/.claude/skills/enough
```

Or for a single project, clone into `.claude/skills/enough` inside the repo.

### Claude.ai / Claude Desktop

Go to **Settings → Capabilities → Skills**, and upload the skill (zip this folder, or grab the release zip). Skills require a paid plan with code execution enabled.

## Use

Just talk to Claude the way you already do:

> "I'm building a tool where freelancers send clients a branded portal with proposals, contracts, invoices, chat, client accounts, payments, analytics…"

> "My side project has been 'two weeks from done' for six weeks. Here's what's left: …"

> "11 users asked for a mobile app. Should I build it?"

> "How's the proposal-pages project tracking against the spec we wrote in May?"

> "I haven't opened this repo in a month. What do I do?"

> "I have 14 users at ₹499/mo. Should I add an agency tier and a free tier?"

The skill triggers on its own. If you want to invoke it explicitly: *"Run this through enough."*

## What an output looks like

> **VERDICT: SHIP AFTER — 9 hours. You've been done for six weeks; the list grew to protect you from launching.**
>
> **True blockers (9 hrs):** pricing page + payment link (4h, money) · import failure message (3h, honesty) · data deletion path (2h, legal floor)
>
> **Felt blockers, cut:** Beehiiv API (one-more-feature — trigger: 5 paying users ask) · tests (write them against real users' cursed CSVs, not your imagination) · import rework ("feels clunky" — six weeks of feelings, zero user reports; ship it clunky)
>
> **Definition of Done:** a writer you've never spoken to uploads their export, sees their best send time, and pays — while you're asleep.

Three full worked examples are in [`examples/`](examples/) — a two-sided marketplace cut from 3 months to 10 days, the "almost done" SaaS above, and a feature-request triage.

## Structure

```
enough/
├── SKILL.md                            # Core: philosophy, modes, ledger, cut tests, voice
├── references/
│   ├── pre-build.md                    # Enough Spec methodology + adversarial preemption
│   ├── mid-build.md                    # Ship Verdict methodology (the 48-hour rule)
│   ├── post-launch.md                  # Feature Triage + the evidence ladder
│   ├── drift-audit.md                  # Drift Audit methodology (NEW in v2)
│   ├── sunset.md                       # Sunset Verdict methodology (NEW in v2)
│   ├── pricing.md                      # Pricing Verdict methodology (NEW in v2)
│   ├── ledger-format.md                # .enough/ directory schema (NEW in v2)
│   ├── cut-patterns.md                 # 18 overbuild patterns and their substitutes
│   └── domains/
│       ├── b2b-saas.md                 # B2B SaaS pack (NEW in v2)
│       ├── consumer.md                 # Consumer / Mobile pack (NEW in v2)
│       └── creator.md                  # Creator / Content pack (NEW in v2)
├── templates/                          # Output templates for all six modes
└── examples/                           # Full worked examples
```

## What v2 changed

- **The Ledger** — every verdict persists to `.enough/`. The skill is now longitudinal.
- **Three new modes** — Drift Audit, Sunset, Pricing.
- **Domain packs** — three personas (B2B SaaS, Consumer, Creator) recalibrate the cut tests and add domain-specific overbuild patterns.
- **Adversarial preemption** — every Enough Spec ships with the rebuttals to the reversal attempts you'll make in week 2.
- **The Builder Profile** — patterns the skill notices across your projects (e.g., "you over-build admin dashboards") get used inline in future verdicts, when the host has a memory system.
- **The signed commitment** — every spec is signed. Future audits quote the signature back when cuts are reversed.

The single change that does the most work is the Ledger. It is what turns the skill from an oracle (one-shot judgment, easily ignored) into an advisor (longitudinal, holds the line over weeks).

## Philosophy

The name carries the whole product. *Enough* as sufficiency — you have what you need to ship. *Enough* as a boundary — that's enough, stop adding. *Enough* as a verdict — this project has had enough of your time; let it go. The skill enforces all three.

It is ruthless about scope and never about the person. The builder's instinct to build is the asset; it's the aim that's off.

## Contributing

PRs welcome — especially:

- New cut patterns (`references/cut-patterns.md`) with real substitutes that shipped
- New domain packs (`references/domains/`) — marketplace, hardware, AI wrapper, agency/services — each with persona truths, recalibrated cut tests, and 5–7 domain-specific overbuild patterns
- Worked examples from real projects, including post-Sunset retrospectives (rare, valuable)

Keep the voice: verdict first, every cut explained, numbers over adjectives, the Ledger is sacred.

## License

MIT — see [LICENSE](LICENSE).

---

*Built by [Tanuj Rajput](https://tanujrajput.com). If this skill kills a feature you loved, it worked. If it sunsets a project you couldn't let go of, it worked harder.*
