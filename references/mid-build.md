# Mid-Build Mode — The Ship Verdict

Use this mode when the user is partway through building and asks some version of "is this ready?", "what's left?", or — the classic tell — has been "almost done" for more than two weeks. The output is a **Ship Verdict**: SHIP NOW, SHIP AFTER (a short, hour-estimated list), or NOT ENOUGH YET (rare).

The hidden truth of this mode: builders asking "is it ready?" are almost never blocked by missing features. They're blocked by fear wearing a feature costume. The job is to separate **true blockers** from **felt blockers** and force the call.

## Method

### Step 1 — Reconstruct the Core Loop

Before judging readiness, establish what "ready" means: state the hypothesis and the Core Loop from what the user has shared (or ask the single question "what's the one path a user takes to get value?"). Readiness is measured against the loop — not against the feature list, the competitor, or the builder's taste.

### Step 2 — Walk the loop against what exists

Step through the loop and mark each step: **works**, **works with rough edges**, or **broken/missing**. Only this walk matters. A project can be 40% of its feature list and 100% of its loop — that ships. A project can be 90% of its feature list with a broken payment step — that doesn't.

### Step 3 — Classify every remaining item

Take the user's "what's left" list (and the unstated items implied by their worry) and sort each into:

**True blockers** — only four things qualify:
1. A Core Loop step is broken or missing.
2. Money: charging fails, double-charges, or can't refund.
3. Data: user input can be lost, leaked, or exposed.
4. Honesty: the landing page promises something the product doesn't do.

**Felt blockers** — everything else, named for what it is:
- *Polish* — animations, empty states beyond the loop, design tweaks, dark mode.
- *Edge cases* — failure paths a first user is unlikely to hit. (Error states ON the happy path are Trust; error states off it are Later.)
- *Infrastructure* — refactors, test coverage, CI, "cleaning up the code." The code is allowed to be embarrassing; it is not allowed to be unshipped.
- *Settings & options* — configurability is a tax users pay for the builder's indecision. Pick the default; ship the default.
- *One-more-feature* — the new idea that arrived last week and now feels essential. It isn't; it's novelty. Log it as LATER.
- *Fear in costume* — "I should add onboarding first," "needs more testing," "let me redo the landing page." If the item has already been redone once, it's this.

### Step 4 — Apply the 48-hour rule

Sum the honest hour-estimates of the true blockers.

- **0 hours of true blockers → SHIP NOW.** Today. Give the literal next action ("flip the DNS, post the link in the two communities you named").
- **≤ 48 working hours → SHIP AFTER.** List the items (3 max), each with an hour estimate, and a ship date. Nothing may be added to this list. If something new comes up, it swaps in by removing something else.
- **> 48 hours of true blockers → the scope is wrong, not the timeline.** Re-run Pre-Build mode on what remains: cut loop steps, fake them manually, or narrow the persona until the remainder fits inside 48 hours. NOT ENOUGH YET as a verdict is reserved for a genuinely incomplete loop that can't be manually faked — it should be rare, and it must come with the cut that fixes it.

### Step 5 — Prescribe the launch floor

"Ship" needs a definition or it slips too. Default launch floor: the product is reachable at a URL, a stranger can complete the loop unassisted, money (if charged) lands in an account, and the builder has posted it somewhere real users are. A tweet is not a launch; a payment link in front of the target persona is.

## Output template

```markdown
# Ship Verdict — [Product Name]

## VERDICT: [SHIP NOW / SHIP AFTER (X hrs) / NOT ENOUGH YET]

**Core Loop status:** [N of M steps working]
1. [step] — ✅ works / ⚠️ rough / ❌ broken

## True blockers ([total hrs])
- [item] — [hrs] — [which of the four categories]

## Felt blockers (cut from the launch path)
- [item] — [polish / edge case / infrastructure / settings / one-more-feature / fear in costume] — [one-line reason it doesn't block]

## Ship plan
[Date]. [Literal next actions: deploy step, where to post, who to message.]

## Definition of Done
[One sentence.]
```

## Worked example (condensed)

**User input:** "My clipboard AI tool is almost done — core hotkey + paste works, Groq API integrated. Left: settings page for model selection, auto-update system, onboarding tour, app icon redesign, refactor the main process, more error handling, maybe local model support. Two weeks-ish?"

**Verdict-first output:**

> ## VERDICT: SHIP AFTER — 6 hours, not two weeks.
>
> **Core Loop status: 3 of 3 working.** Copy → hotkey → transformed paste. That's the product, and it exists.
>
> **True blockers (6 hrs):**
> - API-key failure state — 2 hrs — honesty: first-run with a bad key currently fails silently; the user must see *why* nothing happened.
> - Crash on empty clipboard — 1 hr — it's ON the happy path; people will hit the hotkey before copying.
> - Landing page claims "works offline" — 3 hrs to remove the claim and adjust copy — honesty. (Removing the claim, not building local models.)
>
> **Felt blockers — cut from the launch path:**
> - Settings page for model selection — settings: pick the best Groq model yourself, hardcode it; you are the settings page.
> - Auto-update — infrastructure: at 0 users there is nobody to update; trigger = first breaking change after 100 installs.
> - Onboarding tour — fear in costume: the product is one hotkey; if it needs a tour, the fix is the copy on the download page, not a tour.
> - Icon redesign — polish: second redesign of an icon nobody has seen.
> - Main-process refactor — infrastructure: the code is allowed to be embarrassing.
> - Local model support — one-more-feature: different product, different bet. LATER, trigger = 10 users ask unprompted.
>
> **Ship plan:** Thursday. Fix the three items, record one 30-second screen capture of the loop, post to the two subreddits and the X audience you've been building.
>
> **Definition of Done:** a stranger downloads it, hits ⌥Space, and pastes a transformed clip without you in the room.
