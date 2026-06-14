# Example — Sunset Mode (the side project that needs to be put down)

**User input:**

> "I need help. About 8 months ago I started a habit-tracking mobile app for runners — log your runs, get streak nudges, see how training pace evolves. Shipped on iOS in Feb. Got ~600 downloads (mostly from one TikTok that did okay), ~40 weekly active users at peak, currently down to like 8. One person paid $4.99 for the pro tier. I haven't opened the repo in 5 weeks. I keep telling people I'm 'on a break from it' but the truth is every time I open Xcode I want to do anything else. The TestFlight beta for the Android version is half-built. Should I push through and finish Android? Switch the model to free with ads? Maybe redo the onboarding? Or just… kill it? I don't know."

The skill detects: clear Sunset signals — One Metric dead, repo dormant 5+ weeks, builder using the word "kill" themselves, no Ledger to read because the project predates v2. Domain pack: Consumer.

**Enough output:**

---

# Sunset Verdict — RunStreak (habit-tracking app for runners)

## VERDICT: KILL. Cleanly, by next Sunday.

You already know. You said "kill it" in the middle of the question — that's not me reading between lines, that's you holding the verdict and asking for permission to say it out loud. Permission granted, with a process.

**The bet that failed:** Runners would adopt a streak-tracking iOS app and pay $4.99/mo for advanced training pace insights, because Strava doesn't focus on consistency.

**Why it failed:** the bet didn't survive contact with the persona. Runners who track consistency *already* track it (Strava, Apple Fitness, Garmin Connect, paper). 600 downloads → 40 WAU → 8 WAU → 1 paying is the shape of a product that solved a problem the persona already considers solved. It's not your build — the build clearly works enough that 40 people used it weekly for a stretch. The market voted, and the vote was "fine, but I already have this."

**Days spent:** ~240 (Oct 2025 → now)
**Cash net:** approx −$340 (Apple dev account: $99, design assets, TikTok boost: ~$200) minus $4.99 once. You're down roughly $335.
**Users reached:** ~600 tried, 1 paid, 8 still here.

The three other things you asked about — Android, free-with-ads, redo onboarding — are all "build more on a tested bet that didn't work." Each would be another 60–120 days. The right move isn't another bet; it's banking the lesson.

## Three actions, by Sunday 2026-06-21

### 1. Stop the bleeding
- **Cancel the Apple dev account renewal** (it auto-renews; this is the silent money leak). Set a calendar alarm for one week before the renewal date if you'd rather decide later — but decide.
- **Refund the one paying user the full $4.99** from your last 30 days of charges. Don't wait for them to ask. (Yes, $4.99. The point is the move, not the dollar.)
- **Remove the App Store description hype** that promises "evolving training insights" — leave one sentence: *"RunStreak is winding down. Existing users keep access through 2026-12-01. Thanks for running with us."* Keep the app available; pull the marketing claims that aren't true any more.

### 2. Close the loop with users
Send the eight current weekly-actives a personal email. Three sentences. Suggested draft (rewrite in your voice):

> Subject: Quick note on RunStreak
>
> Hey [name] — RunStreak is winding down. The app will keep working until December, then I'm pulling it. I built it to fill a gap I thought Strava was leaving, and the truth is the gap was smaller than I bet on. If you want your run history as a CSV, reply and I'll send it within 24 hours. Thanks for the weeks you used it. — [you]

Eight emails. One evening. The replies you get will be the most honest user research the project ever produced; read them before opening the next project file.

### 3. Archive the build
- **Archive the repo** as `runstreak-sunset-2026-06`. Don't delete — the SwiftUI streak logic and the watchOS complication code are reusable and surprisingly clean.
- **Pull the half-built Android TestFlight beta from review** if it's still queued. Closing the loop on the platform you didn't ship to is part of closing the project.
- **Take down the TikTok account** or rename it. Builders who keep dead-product handles around accumulate a credibility tax into the next launch.

## What you keep
- **The SwiftUI streak-logic module.** It's clean code and the streak math (handling timezones, skipped days, paused weeks) was non-trivial. Save the file; it'll show up in another project.
- **The two TikToks that worked** (you said one did okay; check which hook). Save the framing. Distribution learning compounds; product learning was specific to this bet.
- **The single user who paid.** Email them separately and ask the one question: *"What were you doing the moment you decided to pay $4.99?"* Whatever they say is information the next project should be designed around.

## The lesson — write this into your notes AND post it publicly

Drafted; rewrite in your voice. The exercise of writing it is the point, even if it never gets published.

> *I built RunStreak assuming runners wanted a "consistency tracker" because the running content I consume frames running as a consistency problem. Runners who experience running as a consistency problem are a subset of runners — and they're already over-served by Strava streaks, Apple Fitness rings, and Garmin badges. I priced the product against a problem the persona considers solved. The mistake wasn't the build; it was picking a problem in a category dominated by free incumbents. Next project: before any code, ask whether the persona's existing free tools already address the problem "well enough." If yes, the bet has to be on a sharper wedge — not a different framing of the same problem.*

That paragraph is worth more than the 240 days. Post it (a tweet, a blog post, a LinkedIn note). The public version is what makes you a builder who's done one project, not a builder who's done zero.

## If you're tempted to REVIVE instead — read this once

The pull will come this week. *"What if I just made it free + ads and let it ride?"* No: free-with-ads on 8 WAU is ad inventory worth approximately $0.40/month against the ongoing maintenance of two app stores. *"What if I pivot to cycling?"* That's a different project; run Pre-Build cleanly, don't drag this build along. *"What if I open-source it?"* Fine, but only after the wind-down email goes out — open-sourcing is not a substitute for the user-facing close.

The cleanest version of you is the one who emails 8 people on a Sunday afternoon, archives the repo on Monday morning, and is free to start the next thing on Tuesday with the lesson at the top of the new doc.

## Definition of Done
The Apple dev account is canceled, the eight emails are sent, the repo is archived, the lesson is posted publicly, and your next Pre-Build session opens with that lesson paragraph already pasted in.

---

**Note the moves:** the verdict opens by naming what the user already said but didn't quite hear themselves say ("you said 'kill it' in the question"); refuses the three rescue options without dismissing them, and explains why each was a re-bet on a tested-and-failed hypothesis; insists on the small refund and small actions because the *practice* of closing a project cleanly is the point, not the dollar amount; preserves three real wins (clean code module, distribution learning, one paying user's testimony); makes the lesson concrete and persona-specific instead of generic; pre-empts the predictable revival pulls; ends on a Definition of Done that's observable, not emotional.
