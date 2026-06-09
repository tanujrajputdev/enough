# enough

**A Claude skill that tells you when to stop.**

Most products don't die because the builder lacked skill. They die because the builder couldn't answer one question: *what is enough?* Enough to ship. Enough to learn. Enough to stop adding features and start finding users.

`enough` turns Claude into a ruthless scope killer. Feed it an idea, a half-built project, or a feature request — it returns a verdict, not a discussion.

## What it does

The skill operates in three modes and auto-detects which one you're in:

| You say | Mode | You get |
|---|---|---|
| "I want to build X" / paste a PRD | **Pre-Build** | An **Enough Spec** — the smallest version that tests your core hypothesis, with every cut explained and every deferred feature given a trigger condition |
| "Is this ready to ship?" / "almost done, what's left?" | **Mid-Build** | A **Ship Verdict** — SHIP NOW, or SHIP AFTER an hour-estimated list of true blockers (max 48 hours of work, by rule) |
| "Should I add this feature?" / "users are asking for X" | **Post-Launch** | A **Feature Triage** — BUILD / DO MANUALLY / WATCH / NO, graded against an evidence ladder |

Every output ends with a one-sentence **Definition of Done** — the observable state that means "stop building, start selling."

## The opinions baked in

This skill is not neutral. It believes:

- **Enough = the smallest version that generates real evidence about the core hypothesis.** Not the smallest version that's impressive.
- Every feature must survive five cut tests: the loop test, the walk-away test, the ego test, the concierge test, and the spreadsheet test.
- "Builders asking *is it ready?* are almost never blocked by missing features. They're blocked by fear wearing a feature costume."
- The default answer to a new feature is **no**. The burden of proof is on the feature, never on the status quo.
- But "enough" is never a license to ship broken: payment integrity, data integrity, honesty, the legal floor, and core-path accessibility are uncuttable.

It also ships with a library of 18 **cut patterns** — auth systems, admin dashboards, settings pages, multi-tenancy, the pre-launch rewrite — the features every bloated spec contains, each with the cheaper substitute that should ship instead.

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
├── SKILL.md                          # Core: philosophy, modes, cut tests, voice
├── references/
│   ├── pre-build.md                  # Enough Spec methodology
│   ├── mid-build.md                  # Ship Verdict methodology (the 48-hour rule)
│   ├── post-launch.md                # Feature Triage + the evidence ladder
│   └── cut-patterns.md               # 18 overbuild patterns and their substitutes
├── templates/                        # Output templates for all three modes
└── examples/                         # Full worked examples
```

## Philosophy

The name carries the whole product. *Enough* as sufficiency — you have what you need to ship. *Enough* as a boundary — that's enough, stop adding. The skill enforces both.

It is ruthless about scope and never about the person. The builder's instinct to build is the asset; it's the aim that's off.

## Contributing

PRs welcome — especially new cut patterns (`references/cut-patterns.md`) with real substitutes that shipped, and worked examples from real projects. Keep the voice: verdict first, every cut explained, numbers over adjectives.

## License

MIT — see [LICENSE](LICENSE).

---

*Built by [Tanuj Rajput](https://tanujrajput.com). If this skill kills a feature you loved, it worked.*
