# Domain Pack — Consumer (Web & Mobile)

Apply this pack when the persona is an individual buying for themselves, not for a company. Detect from the brief: B2C, personal tool, mobile app, social, dating, fitness, productivity-for-self, journaling, content consumption, gaming, finance-for-self.

The consumer overbuild instinct is *engagement theater* — building like the product needs to addict the user before it has been useful to them once. Cut accordingly.

## The persona truths that change cuts

- **Consumers don't think about your product when they're not using it.** Notifications, retention emails, streaks — pre-PMF, these are inventions of "engagement" before the product has been worth opening once. The first user opens the product because they have the problem *right now*; everything else is hope.
- **Day-1 value beats Day-30 retention.** Consumer products that fail to deliver value in the first session are dead, regardless of what month-3 retention "could be." Optimize the first ten minutes; defer everything else.
- **Friction kills, but so does ambiguity.** Sign-up walls fail one way; empty-state walls fail the other. The fix is rarely "remove signup"; it's "deliver value before signup, then ask for an email when the user wants the value to persist."

## Cut tests, recalibrated for Consumer

1. **Loop test — measured in minutes, not sessions.** The Core Loop must close in one session, ideally one minute. If it closes "over the first week" — that's the bet failing, not the loop succeeding.
2. **Walk-away test — measured against habit, not features.** Consumer products replace a habit (Notes, Notion, Instagram, the phone's default app). Test walk-away as: *would the user replace the existing habit, or just add yours on top?* "Add on top" products die when life gets busy.
3. **Concierge test — narrower than B2B.** Consumer users won't tolerate "we'll do it for you over WhatsApp" for long; the product has to actually work. But pre-launch, the *audience* concierge is enormous: hand-DM the first 50 users from the persona's community, get them in, watch them use it.
4. **Ego test — extra weight.** Consumer products are the most ego-prone domain in the skill. Custom animations, brand systems, splash screens, dark mode launches, "delightful" empty states — these are nearly always cuts.

## Overbuild patterns specific to Consumer

In addition to the general `cut-patterns.md`:

### Native iOS + Android launch
- **Why:** "Consumer = mobile."
- **Fails:** loop test ×2 platforms; two app stores; two review queues; two codebases.
- **Ship instead:** responsive web first. Or: one platform, the one the persona lives on. If 80% of the persona is iOS, that's the launch; Android is LATER with a real trigger (≥5 Android users requesting access via the web).

### Onboarding tutorial / coachmarks
- **Why:** the first session shows people the product, so it absorbs the fear.
- **Fails:** loop test; a tutorial is an apology for an unclear first screen.
- **Ship instead:** the first screen IS the tutorial — a single example pre-loaded that the user can interact with immediately, with the result visible. No "next, next, next" overlays.

### Profile / avatar / username system
- **Why:** "social products have profiles."
- **Fails:** loop test until there's a reason for users to see each other.
- **Ship instead:** no profiles at all. Display name only when the user types something into a shared surface. Trigger to build profiles: users in a shared surface ask "who is this?"

### Notifications and streaks
- **Why:** "engagement."
- **Fails:** evidence ladder + walk-away test; pre-PMF, notifications burn the audience you spent so hard to acquire.
- **Ship instead:** one email — the result of the user's last interaction, if they didn't see it. Trigger to build a notification system: the One Metric proves users want the product and forget to come back.

### Social features in a single-player product (sharing, friends, leaderboards, follower model)
- **Why:** "viral loops."
- **Fails:** sequencing — virality requires content already valuable to receivers. Pre-PMF, the value isn't proven, so the virality engineering compounds nothing.
- **Ship instead:** a single shareable artifact (image / link / receipt) at the loop's payoff moment. If the artifact is worth sharing on its own, that's the social layer.

### Multi-platform sync at launch
- **Why:** "users have multiple devices."
- **Fails:** loop test on the second device until the first device is loved.
- **Ship instead:** one platform, local-only or single-device. Trigger to sync: a paying user complains in writing that their data isn't on their other device.

### Subscription before the product is loved
- **Why:** App Store advice; "consumer subscriptions are the model."
- **Fails:** evidence ladder; consumer users hate monthly subscriptions to products they've used three times.
- **Ship instead:** one-time price OR free with a sharply-walled premium feature. Trigger to introduce monthly: ≥30 free users use the core loop weekly for 4 weeks.

### Dark mode / theming / personalization at launch
- **Why:** ego.
- **Fails:** ego test, cleanly.
- **Ship instead:** one good default, ideally the one the persona's existing favorite app uses.

## The One Metric for Consumer

Pre-PMF: *N users who complete the loop and return within 7 days*. Returning is the only thing that separates a real consumer product from a viral demo.

If the product is paid up front (one-time or subscription): *N strangers who pay and then return*. Payment is necessary but not sufficient.

Kill Criteria default: *if fewer than 20% of users who try it complete the loop in their first session, the loop is too long; if fewer than 30% who complete it return within 7 days, the bet is wrong.*

## The Trust layer for Consumer

- **The first screen does what the page promised.** Consumer attention is one screen wide; promise and product have to align in the first 5 seconds.
- **Account recovery exists.** Email-link login means people will lose access if the email bounces; have a path back in.
- **Data export.** Even consumers — especially if the product holds personal data (notes, photos, finances, journals).
- **No dark-pattern subscriptions.** Cancel must be one click from the product, not three from the App Store.

## What an Enough Spec looks like in this domain

A Consumer Enough Spec almost always reads:

- **CORE:** one screen that does the one thing in <60 seconds.
- **TRUST:** payment (if paid), account recovery, data export, honest first screen.
- **LATER:** mobile app (if shipped web), notifications, profiles, sharing, theming, multi-device sync.
- **NEVER (for now):** social features, gamification, streaks, dark mode, multi-platform launch, complex onboarding, second persona.

If the user's spec has profiles, social, notifications, and a mobile app in CORE for a product that doesn't yet have one user who loves it — that's the deepest cut. Make it bluntly.
