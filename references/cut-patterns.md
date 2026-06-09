# Cut Patterns — The Overbuild Library

The same dozen-odd features appear on almost every bloated spec, because they're what "real products" have — and copying real products is how builders avoid the scarier work of finding users. This file lists each pattern, why it shows up, the test it fails, and the substitute that ships instead. Reuse the substitutes verbatim in cut lists.

When reviewing any feature list, scan for these by shape, not name: a "Workspaces" feature is multi-tenancy, a "Preferences" screen is settings, "Activity feed" is notifications.

## The patterns

### 1. Custom auth system (signup, login, password reset, profiles, OAuth)
- **Why it appears:** feels like the foundation; tutorials all start here.
- **Fails:** loop test — value almost never requires identity on day one.
- **Ship instead:** no accounts at all if possible (the paid link / the emailed result IS the identity). If state must persist: magic-link email auth via a hosted provider (Supabase/Clerk), one field, no passwords ever. Profiles: never at launch.

### 2. Admin dashboard
- **Why:** the builder wants to feel like an operator.
- **Fails:** concierge test — the builder can read the database.
- **Ship instead:** SQL console, a Supabase/Metabase view, or a daily metrics email cron. Trigger to build: a non-technical person joins ops.

### 3. Analytics dashboard (user-facing)
- **Why:** charts demo well; screenshots look like a product.
- **Fails:** ego test, usually; users at this stage want the outcome, not graphs about it.
- **Ship instead:** one weekly email with the 2–3 numbers that matter. Trigger: users ask to slice the data themselves.

### 4. Settings / preferences page
- **Why:** the builder couldn't decide, so the user is made to.
- **Fails:** loop test — options are deferred decisions, and every option doubles the test surface.
- **Ship instead:** pick the best default and hardcode it. Each setting earns its way in individually via rung-3 evidence (see post-launch.md).

### 5. Onboarding flow / product tour
- **Why:** fear that the product is confusing — which is information, not a feature request.
- **Fails:** loop test; a tour is an apology for an unclear loop.
- **Ship instead:** fix the empty state and the first-screen copy; pre-fill an example. If the loop needs a tour, shorten the loop.

### 6. Notification system (in-app feed, push, digests)
- **Why:** "engagement."
- **Fails:** concierge + spreadsheet tests, plus a heavy maintenance tail.
- **Ship instead:** one transactional email at the loop's payoff moment, hand-written template. Trigger: users miss payoff moments and say so.

### 7. Multi-tenancy / teams / workspaces / roles
- **Why:** "agencies might buy it"; B2B fantasy revenue.
- **Fails:** walk-away test at zero users; among the most expensive cuts to reverse later, but still wrong on day one.
- **Ship instead:** single-user product; teams share a login (they genuinely will). Trigger: 5 paying users ask to add a teammate, or prepayment for seats.

### 8. Mobile app (when the product isn't inherently mobile)
- **Why:** "everyone's on their phone."
- **Fails:** loop test ×2 platforms; doubles everything.
- **Ship instead:** responsive web. If capture-on-the-go is the actual need: a WhatsApp/Telegram bot or an email-in address, in days not months.

### 9. Integrations (Slack, Zapier, CRM, "API access")
- **Why:** sounds enterprise; one user mentioned Zapier once.
- **Fails:** evidence ladder + permanent maintenance tail (someone else's API, breaking on their schedule).
- **Ship instead:** CSV export covers 80% of integration demand. Then a Zapier webhook before any native integration. Native: rung-4 evidence only.

### 10. Billing portal (plans, upgrades, invoices, proration)
- **Why:** "what if someone wants to upgrade?"
- **Fails:** concierge test — at <100 customers, billing edge cases are emails.
- **Ship instead:** one price, one Stripe/Razorpay/Lemon Squeezy payment link, refunds by hand. Trigger: billing emails exceed ~3/week.

### 11. Search
- **Why:** every app has a search bar.
- **Fails:** loop test until users have months of accumulated data.
- **Ship instead:** reverse-chronological list + browser Ctrl-F. Trigger: real users with real data say they can't find things — then build *filters* first; filters are usually what "search" means.

### 12. Internationalization / multi-currency / multi-language
- **Why:** "the market is global."
- **Fails:** the hypothesis names one persona in one market; i18n multiplies every future string forever.
- **Ship instead:** one language, one currency — the persona's. Trigger: paying users in a second market, in their words.

### 13. Dark mode
- **Why:** builders live in dark mode and build for themselves.
- **Fails:** ego test, cleanly.
- **Ship instead:** one good light theme (or one good dark theme — pick the persona's). Trigger: honestly, almost never pre-revenue.

### 14. AI features bolted onto a non-AI product
- **Why:** 2024–2026 happened.
- **Fails:** ego test / investor-theater; if the loop didn't need it, it's decoration.
- **Ship instead:** nothing — unless the hypothesis itself is about the AI capability, in which case it's CORE and everything *around* it gets cut instead.

### 15. The rewrite / refactor / migration ("just need to move it to Next.js first")
- **Why:** rewriting is comfortable; shipping is exposing.
- **Fails:** loop test — users cannot perceive the framework.
- **Ship instead:** ship on the embarrassing stack. Trigger for refactors: a specific feature is blocked by specific code, named in writing.

### 16. Landing page perfectionism (redesign #3, brand system, animation pass)
- **Why:** the page is the only part strangers have seen, so it absorbs all the fear.
- **Fails:** the second redesign before launch is always fear in costume.
- **Ship instead:** headline that states the promise, one screenshot or 30-second capture of the loop, one button. Trigger for redesign: traffic exists and doesn't convert.

### 17. Waitlist mechanics, referral loops, gamification
- **Why:** growth-hacking content.
- **Fails:** ego test — virality engineering for a product with no proven core value compounds nothing.
- **Ship instead:** charge money on day one; payment is the only waitlist that tells the truth.

### 18. SEO/content engine before product signal
- **Why:** "build the audience while building the product."
- **Fails:** sequencing — content compounds toward a hypothesis; an unproven hypothesis means compounding in a guessed direction.
- **Ship instead:** direct outreach to 50 named people in the persona. Slower-looking, faster-learning. Trigger for content engine: the One Metric shows signal.

## Reading a spec with this library

A quick severity heuristic when several patterns co-occur: one or two patterns is normal builder reflex — cut and move on. Five or more, or any appearance of #7 (multi-tenancy) or #15 (the rewrite) pre-launch, signals the deeper issue: the builder is using the build to avoid the market. Say that gently and directly — it's the single most valuable cut this skill makes.
