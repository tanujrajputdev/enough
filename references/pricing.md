# Pricing Mode — The Pricing Verdict

Use this mode when the user asks any version of "what should I charge?", "is this too expensive?", "should I add a free tier?", "should I do a lifetime deal?", or shares a pricing page with three tiers and a question mark. The output is a **Pricing Verdict**: one specific price, or one specific change to existing pricing — never "it depends on your positioning."

Most pre-PMF builders make the same three pricing mistakes: they price too low, they ship three tiers when they need one, and they add a free tier to "reduce friction" that ends up costing them every paying user's attention. This mode names which one is happening and prescribes the cut.

## When this mode runs

- Pre-launch: the user is about to ship and doesn't know what to charge.
- Post-launch under signal: the user is making money but suspects they're under-priced.
- Pricing page redesign: any time the user wants to add a tier, the answer should usually be "remove one instead."
- Free → paid transition: the hardest pricing change a builder makes; this mode forces it.

## The four pricing truths the skill enforces

1. **One price beats three tiers, pre-PMF.** Three tiers force the user to think about positioning, packaging, and feature gating before they know who the customer is. One price forces them to find out.
2. **Free tiers are a tax on paid users.** Every free user takes support, hosting, and edge-case load without paying for it. Pre-PMF, the cheapest possible "free tier" is *a 7-day money-back guarantee on the paid product*. No free tier; no free trial that requires a credit card and then doesn't charge; just charge.
3. **Annual pricing is for proven retention.** Offering an annual discount when month-2 retention is unknown is bribing users to lock in before you know the product holds. Trigger to add annual: ≥3 months of cohort data showing month-3 retention >60%.
4. **Round numbers beat .99 endings.** Pre-PMF, the buyer is deciding whether to trust you at all; ₹999 reads "we picked a price"; ₹997 reads "we read a copywriting book." Save psychological pricing for when the funnel is mature enough that 0.5% matters.

## Method

### Step 1 — Read the Ledger and the persona

Pull from the latest spec: the hypothesis, the persona, the One Metric. Pricing has to be tested against persona, not against the builder's salary expectations.

If there's no Ledger and the user is asking about pricing, ask the one permitted question: *"Who's the customer, and what's the alternative they're using today that costs them money or time?"* Pricing without a persona is taste.

### Step 2 — Find the floor and the ceiling

The skill computes two numbers, not from market research, but from the persona's existing spend.

- **Floor** = the cost of the cheapest workaround the persona uses today. If freelance designers use a $12 PDF tool + a $9 Stripe link tool + a Notion template, the floor is ~$25/mo.
- **Ceiling** = 10% of the value the persona is creating with the workflow this product replaces. If the workflow gets them paid for ₹50,000 of work per month, ₹5,000/mo is the ceiling.

Most pre-PMF prices belong between the floor and 30% of the ceiling. Below floor: the persona didn't realize there was a price to compare against. Above 30% of ceiling: the persona starts comparing the tool to hiring a person.

### Step 3 — Decide the move

Five common situations; pick the matching verdict.

- **No pricing yet, pre-launch:** *one price between floor × 1.5 and ceiling × 0.2. One Stripe/Razorpay/Lemon Squeezy link. No free tier. No trial. Money-back guarantee, 7 days, advertised on the page.*
- **Free + paid, fewer than 100 paid users:** *kill the free tier today.* Existing free users keep access until they take a destructive action (export, delete); new users must pay. Cite cut-patterns #17 (waitlists) for the principle: payment is the only signal that tells the truth pre-PMF.
- **Three tiers, fewer than 50 paid users on the middle tier:** *kill the bottom tier and the top tier. Keep the middle.* The bottom tier hides the value; the top tier was for the customer you don't have yet. Trigger to bring back the top tier: 10 paying users ask for the top-tier feature unprompted.
- **Paying users above 30, price feels low ("nobody pushes back on it"):** *raise to 1.5× immediately for new customers, grandfather existing.* No-pushback is information; the price is below the floor and the persona knows it. Email existing users with the change and the date.
- **User wants to add lifetime deal / AppSumo:** *no, unless three things are true:* (1) the product has shipped, (2) the One Metric proves users get value, (3) the lifetime price is calculated as 18+ months of regular revenue, not "whatever the deal site wants." Otherwise: lifetime deals destroy the LTV math and bring users who will outlast your patience.

### Step 4 — Write the migration plan (if there's existing revenue)

A pricing change for existing users is a Trust-layer event. Always:

- **Email existing users by name** at least 14 days before the change. The skill drafts this email — not a notice, not a banner.
- **Grandfather existing paying users at their current price** for at least 12 months — or honestly, forever, if the user base is under 100. The headline of pre-PMF pricing isn't revenue; it's the willingness of strangers to pay anything.
- **Don't change the price for users in the middle of a billing cycle.** The new price applies to the next renewal.

Free-tier removal is an exception: free users get an email, a 30-day window, and a clear upgrade path. They don't get grandfathered, because they were never paying.

## What never gets priced

- **Honesty on the page.** If the price is ₹999, the page says ₹999, with VAT/tax handling stated. No "starting from" without a number.
- **Refunds.** If you take money, charge cleanly and refund cleanly. Refund policy must exist before you take the first payment.
- **Currency clarity.** State the currency; "$" without "USD" is sloppy when half the buyers are in another country.

## Output template

See `templates/pricing-verdict-template.md`.

## Worked example (condensed)

**User input:** "My CRO audit tool has 14 paying users at ₹499/mo. I'm thinking of adding a ₹1,499 'agency' tier with white-label, and a free tier to grow the funnel. Thoughts?"

**Verdict-first output:**

> ## VERDICT: One price. Raise it to ₹1,499. No new tiers. No free tier. By Monday.
>
> **What you have:** 14 payers at ₹499/mo = ₹6,986/mo. The price is below your floor.
>
> **Floor for this persona:** an agency owner running CRO experiments is already paying ~₹2,000–3,000/mo across Hotjar/Microsoft Clarity/manual analyst time. ₹499 reads "free" to them, which is why they're not telling anyone about you.
>
> **Ceiling:** a single CRO win for an agency client is ₹50,000–₹200,000 in retained revenue. 10% of the low end is ₹5,000/mo. You have plenty of room to triple.
>
> **The cut, in order:**
> 1. **New price: ₹1,499/mo, single tier.** No agency tier. The "agency tier" was the original product all along; you priced the original product as the entry-level tier by accident.
> 2. **No free tier.** Cut-pattern #17 applies: payment is the signal that tells the truth. The 30 free users you're imagining acquiring would consume 80% of your support hours.
> 3. **Grandfather the 14 existing payers at ₹499 forever.** They believed first. Don't punish that.
> 4. **Money-back guarantee: 14 days, on the page.** Removes the only reasonable objection at the new price.
>
> **What to send to existing users (verbatim):**
>
> > Subject: Pricing change for new customers — your price doesn't change
> >
> > Hey [name], a heads-up: starting Monday, new signups will be ₹1,499/mo. **Your price stays at ₹499 as long as your subscription stays active** — you got in early and that matters. If you ever cancel and come back, you'd come back at the new rate. That's it. Thanks for being one of the first 14. — [you]
>
> **What to put on the page:** *₹1,499/mo. 14-day money-back guarantee. Used by 14 agencies running ~120 audits/month.* Social proof from the existing 14 is the strongest part of your pitch and you weren't using it.
>
> **Definition of Done:** the next new customer pays ₹1,499 by Monday, and one existing user replies to the email saying "no problem, thanks for the heads up."

Note the shape: one price, the floor and ceiling math shown briefly, the verbatim user email so the user doesn't slip on the Trust layer, and a Definition of Done that's a single observable event.
