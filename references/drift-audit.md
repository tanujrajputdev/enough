# Drift Audit Mode — The Hold-the-Line Check

Use this mode when the builder has a `.enough/` Ledger and asks for a status check, or when the skill detects auto-fire conditions (below). Output is a **Drift Audit**: a verdict — *ON TRACK / DRIFTING / TIME TO SUNSET* — with the exact items that drifted and the one move that fixes the week.

The Drift Audit is what makes `enough` longitudinal. A spec the builder ignores is just a wishlist. A spec that gets audited is a commitment.

## When this mode runs

Run a Drift Audit when **any** of the following is true:

1. The user asks for one ("how's the project doing", "am I on track", "drift check", "audit this").
2. The user starts a new session and the Ledger has a `spec` whose deadline is within 7 days, or already past.
3. The latest spec is >7 days old and no audit has been written since.
4. The user opens a Mid-Build session ("is this ready?") — auto-prepend a quick drift audit before the Ship Verdict.
5. The user tries to add a new feature or open a new mode on a project whose Ledger shows a stalled `spec` (no commits in 5+ days, or deadline already passed).

If no `.enough/` Ledger exists, this mode does not run. Offer to start one by re-running Pre-Build mode.

## Method

### Step 1 — Read the Ledger

Read the latest `spec` file in `.enough/`. Extract: hypothesis, Core Loop, CORE list, TRUST list, LATER list (with triggers), NEVER list, One Metric, Kill Criteria, deadline, signed_by.

If a more recent `ship` or `triage` exists, read those too — they may have legitimately promoted LATER items or rebalanced scope. Audit drift against the *latest committed verdict*, not just the original spec.

### Step 2 — Read reality

The skill checks four sources, in this order, stopping at whichever is sufficient. None are required; missing sources just narrow the audit.

**Git** (always, when the project is a git repo):
- `git log --since="<spec.created>" --pretty=format:"%h %ad %s" --date=short` — commit history since the spec
- `git log -1 --format=%cd --date=short` — date of last commit
- `git ls-files | wc -l` — file count now vs at spec time (approximate via `git rev-list HEAD --count` and file count at spec commit if findable)
- `git diff --name-only <spec-commit>..HEAD` — files changed since the spec

**The file tree**:
- New top-level directories since the spec? (Sign of unplanned scope.)
- New entries in `package.json` / `requirements.txt` / `go.mod`? (Dependency growth = scope growth.)
- Files matching the NEVER list by name or path? (Cut features sneaking back.)

**The Ledger's One Metric**, if measurable:
- A `enough.config.yaml` at the repo root may point at a metric source (a Stripe export CSV, an analytics file, a payments count file). Read it if present.
- If absent, ask the user once: *"What's the current value of the One Metric?"* Take their answer at face value and proceed.

**The user's own report** for everything else. Don't interrogate; one question maximum.

### Step 3 — Score four drifts

For each dimension, decide *acceptable / drifting / dead* with a number, not a vibe.

**Cut drift** — features the Ledger said cut, but code shows partly built.
- Walk the NEVER list against the file tree. Match by shape: `/src/admin` or `/app/dashboard/admin` is the admin dashboard from cut-pattern #2 regardless of name.
- Walk the LATER list. If a LATER item appears in code without its trigger having fired, that's drift. (Triggers are written down; check them honestly.)
- Output: each drift named, file location given, verdict — *restore the cut* or *promote with a one-line reason*.

**Deadline drift** — days slipped vs the spec's deadline.
- 0 days slipped → on track.
- 1–3 days → soft slip; flag but don't sound alarms.
- 4+ days → hard slip; extend once with a new deadline OR cut more scope. Two extensions in one project is the sunset signal.
- Already past deadline with no ship → run the calculus for sunset.

**Metric drift** — actual One Metric value vs Kill Criteria thresholds.
- On pace (linear projection hits the threshold): *on pace*.
- Behind but moving: *behind, here's the gap*.
- Past Kill Criteria deadline with metric below threshold: *dead per the builder's own signed criterion*. Route to Sunset Verdict.
- Above threshold already: *bet won; this project graduates to Post-Launch mode for new triage*.

**Velocity drift** — is the project actually moving?
- Commits in last 7 days: 0 = stalled, 1–3 = slow, 4+ = moving.
- Last commit >14 days ago on a pre-ship project: this isn't drift, it's dormancy. Route to Sunset.

### Step 4 — Issue the verdict

Three verdicts, no fourth:

- **ON TRACK** — no drifts above "soft," velocity moving, metric on pace or ship not yet due. Output is short: confirm the spec is holding, name the one item to attack this week.
- **DRIFTING** — one or more hard drifts. Name them, prescribe the fix. The fix is always *cut harder, ship faster, or sunset*. Never *add scope to recover*.
- **TIME TO SUNSET** — metric dead per signed Kill Criteria, OR deadline slipped twice, OR no commits in 21+ days. Don't render the Sunset verdict here; route the user to Sunset mode with the specific reason.

### Step 5 — Prescribe one move

Every Drift Audit ends with exactly one action for the next 7 days. Not three. Not a list. The one thing that, if done, makes next week's audit better.

If you can't name one, the project is in Sunset territory; route there.

## Output template

See `templates/drift-audit-template.md`.

## Worked example (condensed)

**Setup:** Spec signed 2026-06-14 for a branded proposal-pages tool. Today is 2026-07-05 (21 days in). Deadline was 2026-06-26 (deadline +9d). One Metric: 10 paying strangers by 2026-07-05. Current: 2 paying.

**Verdict-first output:**

> ## VERDICT: DRIFTING — and one more week without a verdict swap and you're sunsetting.
>
> **Cut drift (1):** `/app/admin` exists. You cut "admin dashboard" as NEVER on 2026-06-14 with the reason: "you can read the database." Three files in there, last touched 4 days ago. **Restore the cut.** Delete the directory or move it to a branch you don't merge.
>
> **Deadline drift:** Original 2026-06-26. Today 2026-07-05. Slip: +9d. **One extension is allowed; this is it.** New deadline: 2026-07-12. If you don't ship by then, the deadline isn't the problem.
>
> **Metric drift:** 2 paying strangers in 21 days against a Kill Criteria of 10 in 21 days. You are at 20% of signal with 0 days left in the original window. This isn't a fail yet, because you haven't actually shipped — but every day this drags, the kill window resets later, which is how projects become undead. **Ship in 7 days or sunset.**
>
> **Velocity:** 6 commits in the last 7 days, last commit yesterday. You are moving. Good. You're moving on the wrong things.
>
> **The one move this week:** delete `/app/admin`, ship the payment page you already have, post the payment link to the 50-person list you've been growing. By Friday. Nothing else.
>
> **Definition of Done (unchanged from spec):** a stranger pays ₹999 and receives their branded page without you touching anything.

Note the shape: numbers everywhere, the original signed cuts quoted verbatim, exactly one move, and a path to Sunset already named so the next audit isn't a surprise.
