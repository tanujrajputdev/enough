# Example — Pre-Build Mode (two-sided marketplace)

**User input:**

> "I want to build a marketplace where home chefs sell weekly meal subscriptions to busy professionals. Features: chef onboarding with verification, chef profiles with photos and reviews, browse/search with dietary filters, subscription management, delivery scheduling, in-app chat between chefs and customers, ratings system, chef payout dashboard, customer mobile app, referral program, and an admin panel for me. Stack will be Next.js + Supabase. Thinking 3 months to MVP."

**Enough output:**

---

# Enough Spec — HomePlate

**The Enough version is five chefs, one neighborhood, and a WhatsApp-and-payment-link operation. Ship in 10 days, not 3 months.**

The riskier side of this marketplace is demand — chefs who cook for money already exist and are findable; what's unproven is whether busy professionals will *prepay weekly* for a stranger's home cooking. So the spec tests the buyer and fakes everything else.

**The bet:** Busy professionals in [one specific neighborhood] will prepay ₹1,500–2,500/week for a home chef's fixed weekly menu because they're tired of delivery-app roulette and want consistent, home-style food.
**Ship deadline:** 10 days from today.
**Definition of Done:** 1 stranger (not a friend) prepays for week 2 — i.e., they tried week 1 and came back with money.

## The Core Loop
1. Professional sees this week's menus from 5 chefs (one page).
2. Picks a chef, picks a plan, pays.
3. Food arrives on the scheduled days.
4. Next week, they renew.

## Build this (CORE)
- One static page: 5 chef cards, each with photo, this week's menu, price, and a payment link — without it there is no storefront.
- Razorpay payment links per chef-plan — without payment there is no test; "interested" is not data.
- A Google Sheet as the order book — orders, addresses, delivery days. (Yes, this is CORE. The sheet is the backend.)

## Build this minimally (TRUST)
- WhatsApp order confirmation, sent by you, within an hour of payment — prepaying a stranger for food requires a human acknowledgment.
- A refund promise in writing on the page ("don't like week 1, full refund") — removes the walk-away risk of prepayment.
- FSSAI/home-kitchen compliance note — flag: verify what's legally required for home-chef food sale in your city before charging. This is the legal floor, not optional.

## Cut — LATER (build when the trigger fires)
- Chef self-serve onboarding — trigger: more than 15 chefs and your phone-based onboarding breaks.
- Browse/search with dietary filters — trigger: more than ~12 chefs on the page (until then, the page IS the browse).
- Subscription auto-renewal — trigger: 20+ active weekly customers and manual renewal links cost you >2 hrs/week.
- Reviews/ratings — trigger: enough volume that buyers can't just be told "chef Meera's rajma is the move" by you on WhatsApp.

## Cut — NEVER (for now)
- Chef verification system — concierge test: you will personally visit and taste-test 5 kitchens. You are the verification system.
- In-app chat — spreadsheet test: WhatsApp exists and both sides already live there.
- Chef payout dashboard — concierge test: you will pay 5 chefs by UPI every Sunday from the sheet.
- Customer mobile app — pattern #8: responsive page; nobody installs an app to buy dinner from 5 chefs.
- Referral program — pattern #17: virality engineering on an unproven core. The referral program is the food.
- Admin panel — pattern #2: the Google Sheet is the admin panel.
- Customer accounts — the payment + phone number is the account.

## The One Metric
**Week-2 renewals from strangers.** Kill criteria: if fewer than 5 of the first 20 paying customers renew for a second week within 21 days of launch, the bet is wrong — investigate whether it's the food, the price, or the premise before writing more code.

## Manual-for-now plan
You recruit 5 chefs by hand. You collect menus every Sunday over WhatsApp and update the page. You confirm orders, coordinate delivery (chefs deliver or you use Porter/Dunzo per order), handle refunds, and pay chefs weekly. This manual layer is not the compromise — it's the research department.

---

**Note the moves:** two-sided idea reduced to a one-sided test; 11 features became 3 builds and a sheet; the 3-month timeline collapsed because the timeline was holding infrastructure, not the experiment.
