# Changelog

## 0.1.0

- First release. Answers "how can I earn on my USDC" by laying out lending and the two
  options routes as promises rather than rates, then handing off.
- **Never ranks by rate.** Routes on one question — "is there a coin you'd be glad to
  own if it got cheaper?" — and treats a no as a complete answer rather than something
  to counter with a higher number.
- Surfaces the difference most owners miss: Derive settles in **cash**, Rysk delivers
  the **asset**, which are opposite outcomes for someone whose reason was wanting to
  own the asset cheaper.
- Moves no money and files nothing; reads each route live through that skill's own
  helper rather than shipping one or quoting a remembered figure.
