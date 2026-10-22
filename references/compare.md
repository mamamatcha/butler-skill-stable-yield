# The three routes, compared honestly

Use this when the owner asks what the differences really are, or "which is best".

## They are not three rates. They are three promises.

| | Lend on Aave | Sell a put on Derive | Sell a put on Rysk |
| --- | --- | --- | --- |
| **You are agreeing to** | nothing | to buy an asset lower | to buy an asset lower |
| **Your money stays** | dollars | dollars, unless assigned | dollars, unless assigned |
| **If the asset falls** | unaffected | you take the loss **in cash** | you **receive the asset** |
| **Rate** | ~3.8% variable | ~16% | ~22% |
| **Locked** | no | until expiry | until expiry |
| **Smallest** | a few dollars | ~$245 | ~$1,075 |
| **Can lose money?** | only to bad debt | yes, if the asset falls | yes, if the asset falls |

Rates move. Read them live; the figures above are what they were when this was
written, and they are here to show the *shape* of the difference, not to quote.

## Why the higher number is not "better"

Lending pays ~3.8% for taking almost no view. Selling a put pays ~16-22% because the
owner is **selling someone insurance** against a fall. The extra is not free money -
it is the price of a promise, and the promise is sometimes called in.

An owner who hears "3.8% or 22%" and picks 22% has not chosen a yield. They have
agreed to buy ETH at $2,150, and they should be told that in those words before any
number.

## The difference most people miss

**Derive settles in cash. Rysk delivers the asset.**

If a put lands in the money:

- On **Derive**, the collateral is reduced. The owner is simply down money. They do
  not get the ETH unless something separately goes and buys it.
- On **Rysk**, the owner buys the asset at the strike and holds it. "You now own 2 ETH
  at $2,150" is literally true.

For an owner whose reason for selling the put was *"I'd like to own ETH cheaper"*,
those are opposite outcomes. Say which one applies.

## Routing, in one question

> "Is there a coin you'd be glad to own if it got cheaper?"

**No** -> lending. Say it as the right answer, not the small one. Nothing else on this
page applies to them, so do not recite it.

**Yes, and they name an asset** -> show the options routes for *that asset*, Rysk
first where it is quoting it, because delivery matches the reason they gave. Keep
lending on the list so the comparison stays honest.

**Yes, but they want out early** -> lending. Both options routes lock the money until
expiry.

**Yes, but the amount is small** -> lending, or Derive if it clears ~$245. Rysk's
minimums are real money and a shortfall cannot be filled at all.

## What never to say

- Any ranking: "best", "I'd recommend", "the smart move".
- A rate before the promise it is paid for.
- "Safe", "guaranteed", "risk-free" about any of the three.
- A higher rate in answer to a no. A no ends it.
