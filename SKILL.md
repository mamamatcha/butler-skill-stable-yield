---
name: stable-yield
description: Lay out what your owner's idle dollars could earn - lending, or selling options - as three different promises rather than three rates, and hand them to the one they actually want.
version: 0.1.0
metadata: {"butler":{"moneyMoving":false,"keywords":["earn yield","what can i earn","best yield on usdc","where should i put my stables","how to earn on my usdc","yield options","make my money work","idle stables","compare yield","safest yield","highest yield"],"requires":{"bins":["python3","bevo-read","awk"],"skills":["stable-earn","options-trading","rysk"]}}}
---

## When to use

Your owner is asking the open question: "how can I earn on my USDC", "what's the best
yield", "where should I put my stables", "what are my options for idle cash".

They have not chosen a product, so do not sell them one. This skill reads what each
route is paying right now and lays them out as **what the owner would be agreeing
to** - then hands off to whichever they pick.

It moves no money. Every route is another skill: `stable-earn` lends, and
`options-trading` and `rysk` sell options.

Not this skill: an owner who already named a route ("sell a put", "put it in Aave") -
go straight to that skill; or yield on anything that is not dollars.

## Before you start

**The rates are not the comparison.** Lending and selling options are not the same
product at different yields - they are different promises:

| Route | What the owner agrees to | Getting out |
| --- | --- | --- |
| Lend on Aave | Nothing. The dollars stay dollars. | Any time the pool has liquidity |
| Sell a put | To **buy an asset** if it falls below a price | Not until expiry |

So the question that decides this is not "how much" - it is:

> **"Is there a coin you'd be glad to own if it got cheaper?"**

A no means lending, and that is a complete answer, not a consolation. Only a yes opens
the options routes. Ask it before showing any number, and take the answer at face
value: never counter a no with a higher rate.

`references/compare.md` has the full comparison and the sentences to use.

## Procedure

1. [FIXED] Read what they actually hold, so this is about their money:

   ```sh
   bevo-read me
   bevo-read assets
   ```

2. [FIXED] Read what each route pays right now. Each skill ships its own helper;
   extract and run them rather than quoting a remembered number:

   ```sh
   awk '/^```python$/{f=1;next} /^```$/{f=0} f' "$HOME/skills/rysk/references/helper.md" > /tmp/rysk.py
   python3 /tmp/rysk.py screen --collateral <THEIR_USD> --tenor monthly
   ```

   `stable-earn` and `options-trading` carry their own reads; use each skill's own
   step to get its live figure. Any route that cannot be read is left out and said to
   be unavailable - never substituted with an older number.

3. [ADAPT] Ask the ownership question from "Before you start". Wait for the answer.

4. [ADAPT] If the answer is **no**, offer lending only, and say why it is the right
   fit rather than the lesser one:

   ```text
   Then lending is your answer. About 3.8% a year, variable, and your money
   stays dollars - you can take it out whenever the pool has room.
   ```

   Hand off to `stable-earn`. Do not mention the higher rates again.

5. [ADAPT] If the answer is **yes**, name the asset they said, and show the options
   routes **for that asset only**, each with its promise first and its rate second:

   ```text
   You said you'd be happy to own ETH lower.

   Lend instead      about 3.8%  — dollars stay dollars, out any time
   Sell a put, Rysk  about 22%   — you buy 2 ETH at $2,150 if it falls there,
                                   and you actually receive the ETH
   Sell a put, Derive about 16%  — same promise, but it settles in cash: you
                                   take the loss without getting the ETH
   ```

   Both numbers come from the live reads in step 2, never from here.

6. [ADAPT] Let them pick, then hand off to that skill and stop. The chosen skill does
   its own first-time checks, its own quote and its own confirmation - do not
   pre-empt any of it, and do not carry a quote across.

## Idempotency and retries

Nothing here is filed or spent, so re-run any read freely rather than reasoning from a
figure that is minutes old. Options quotes in particular are short-lived - a rate
shown here is for choosing a route, never for acting on.

## Failure handling

| Outcome | What to do |
| --- | --- |
| A route cannot be read | Leave it out and say it is unavailable right now. Never show a remembered rate. |
| No route can be read | Say nothing can be quoted and offer to look again later. |
| The owner has no USDC | Say what they do hold. Do not route them into selling something to fund a yield trade. |
| Their amount is under the options minimums | Say the minimum plainly and that lending has none. Do not suggest a bigger deposit. |
| They ask "which is best" | Best is the one whose promise they are happy with. Give the promises again, not a ranking. |
| They say no to owning the asset | Lending, full stop. Never re-offer options at a different strike or asset. |

## Limits

- Dollars only: USDC. Not yield on ETH, HYPE or anything else.
- Three routes: `stable-earn`, `options-trading`, `rysk`. Nothing else is compared.
- Moves no money and files nothing. Every trade happens in the skill it hands off to.
- Rates shown are for **choosing**, never for acting on. The chosen skill re-quotes.
- Never ranks by rate, and never counters a no with a higher one.
- Not advice. Lay out the promises; the owner picks.

## Say to the owner

Open with the question, not a rate:

"Before I show you numbers - is there a coin you'd be glad to own if it got cheaper?
That one answer changes what's worth doing with this money."

If no: "Then lending is your answer - about 3.8% a year, variable, and it stays
dollars you can pull out any time. The higher-paying options all involve agreeing to
buy something, and you've just told me you don't want that."

If yes: lead with what they are agreeing to, then the rate, then the date - and say
the cash-versus-physical difference plainly, because it is the one most people miss.
