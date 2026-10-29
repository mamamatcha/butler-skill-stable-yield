# butler-skill-stable-yield — retired

> **This skill is retired, and nothing replaces its routing.** Each route is now its own
> skill, found on its own words, with no router choosing between them:
>
> | | |
> | --- | --- |
> | Lending USDC (Aave on Base) | [`stable-earn`](https://github.com/mamamatcha/butler-skill-stable-earn) |
> | Selling a put (Derive, Paradex, Rysk) | `options-trading` ([`butler-skill-yield-notes`](https://github.com/mamamatcha/butler-skill-yield-notes)) |
> | Registry | never listed; nothing installs it |
> | Last version here | 0.1.0 |
>
> Open issues and changes against those repos. This repo is kept read-only so its
> history stays resolvable.

The `stable-yield` skill for [Butler](https://github.com/Virtual-Protocol/butler-skills).
For the humans maintaining this repo — never published to a butler. Only `SKILL.md`
and `references/**/*.md` reach one.

## What it does

Answers the open question — *"how can I earn on my USDC?"* — by laying out the three
routes as **promises rather than rates**, then handing off to whichever the owner
picks. It moves no money and files nothing.

Built on `requires.skills`: `stable-earn`, `options-trading`, `rysk`. The hub installs
those first, so this skill runs **their** helpers for live rates rather than shipping
its own or quoting remembered numbers.

## The design decision

The obvious version of this skill is a league table: 3.8% / 16% / 22%, sorted.

That is the exact failure mode every other skill in this family is built to avoid. An
owner who picks 22% off a ranking has not chosen a yield — they have agreed to buy ETH
at $2,150, and nobody told them in those words.

So the skill **never ranks**, and leads with one question instead:

> *"Is there a coin you'd be glad to own if it got cheaper?"*

A **no** is a complete answer — lending, full stop, said as the right fit rather than
the consolation prize. Only a **yes** opens the options routes, and then only for the
asset they actually named.

## The distinction it exists to surface

**Derive settles in cash; Rysk delivers the asset.** If the put lands in the money,
Derive reduces the collateral and the owner is simply down money — they never receive
the ETH. Rysk hands it over.

For an owner whose stated reason was *"I'd like to own ETH cheaper"*, those are
opposite outcomes, and it is the thing most people miss. `references/compare.md` says
it plainly.

## Not money-moving

Nothing is sent, signed or filed here — every trade happens in the skill it hands off
to, which runs its own first-time checks and its own fresh quote. Rates shown are for
**choosing a route**, never for acting on; options quotes in particular are
short-lived.

## Listing

`requires.skills` means all three of `stable-earn`, `options-trading` and `rysk` must
be listed before this one can be. `options-trading` already is.

## Validating a change

```sh
curl -sSLO https://virtual-protocol.github.io/butler-skills/tools/validate.py
python3 validate.py --standalone .
```

`--all` additionally checks that every skill in `requires.skills` is listed.
