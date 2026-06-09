# Example — Post-Launch Mode ("users are asking for a mobile app")

**User input:**

> "My journaling web app has been live 2 months. 340 signups, 61 weekly actives, 19 paying ($6/mo). I keep getting asked for a mobile app — I've counted 11 requests. I know mobile is a huge lift but 11 requests feels like real demand. Also one user wants Notion export and another suggested mood-tracking charts. Prioritize these for me?"

**Enough output:**

---

# Feature Triage — mobile app, Notion export, mood charts

## VERDICTS: mobile app → DO MANUALLY (there's a manual version of "mobile," and it ships this week) · Notion export → WATCH · mood charts → WATCH

**Original bet:** people will pay $6/mo to keep a private journaling habit.
**One Metric now:** 19 paying — early signal, not proven. 61 weekly actives against 340 signups (18% activation) says the bigger problem is people who sign up and never form the habit, not missing platforms.

---

### Mobile app — evidence rung 3–4, but triage the problem, not the solution

11 unprompted requests out of 61 actives is real signal — the strongest on your list. But "mobile app" is the *solution* users reached for; the *problem* underneath it is almost certainly "I want to journal in bed / on the train, and opening a browser is friction." Eleven people did not ask for Swift; they asked for the journal to be where their thumb is.

**Loop tax / cost:** a native app is 2–3 months for a solo builder plus a permanent second codebase and app-store tail — against a $114/mo product. That math doesn't clear until the metric is proven.

**The manual version of mobile, shipping this week (≈2 days):**
1. **PWA pass** — manifest + service worker + "Add to Home Screen" prompt. Your web app becomes an icon on their phone that opens full-screen. To a journaler, that *is* the app.
2. **Journal-by-message** — a WhatsApp/Telegram/email-in address: anything sent to it lands as an entry. In-bed journaling, zero app stores.

Then message all 11 requesters personally: "You asked for mobile — try this." Their response is your rung-5 evidence. **Promotion trigger for a true native app:** PWA + message-in is live, and paying users still churn citing mobile, and MRR > $1k. All three.

### Notion export — WATCH (rung 2: one ask)

Zero loop tax, small build, but one request is noise. Log it. **Trigger: becomes BUILD at 5 unprompted asks** — and when it fires, the enough version is "Export all entries as Markdown" (Notion imports Markdown; you never touch Notion's API — pattern #9, integrations last).

### Mood-tracking charts — WATCH, and be honest that this one tempts *you* (rung 1–2)

One suggestion, but charts demo well and you can feel the pull (pattern #3, analytics). The risk is real: mood-tracking nudges the product from "private journaling" toward "quantified self" — a different persona wearing a feature costume. **Trigger: becomes BUILD when 5+ *paying* users describe wanting to see patterns in their entries, in their own words.** The one-line reply to send the suggester: "Love it — logging it. What would you want it to show you about your last month?"

---

## Where the next two weeks actually go

Not on any of the three. 18% activation is the fire: of 340 people convinced enough to sign up, 279 never built the habit. Fixing the first-week experience for people who already showed up moves the One Metric more than any feature on this list — and it's also, quietly, the real answer to the mobile requests: friction.

---

**Note the moves:** the strongest request still doesn't get an auto-BUILD — it gets the problem behind it solved at 5% of the cost, with a hard trigger for the expensive version; every WATCH gets a verbatim trigger and a reply to send; and the triage ends by pointing at the metric the features were distracting from.
