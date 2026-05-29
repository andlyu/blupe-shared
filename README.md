# BluPe — Shared Ideas

A living doc for the high-level thesis we're working on at BluPe (Max 500 words).

---

## What we're doing

**The pitch, simply: ease the eval burden through simulation and remote teleop** — so teams
get **10x more rollouts, with more variation, without a person babysitting them.**

Today evals are manual: a policy runs, the environment is reset, over and over. Smaller
teams have **researchers** doing this; larger teams closer to production have
**technicians**. Either way a person is in the loop for every rollout — which caps how many
evals a team runs and pushes them toward small eval sets that don't stress the policy. We
want to take the person out of the loop.

## The approach: simulation + remote teleop

- **Simulation** to continuously validate the model's performance — rough signal that
  might not be 100% accurate, but cheap and always-on.
- **Real-world testing** once a policy is good enough, then **continuous testing in
  deployment.**

How far testing can move into sim is unclear, but labs test heavily in the real world
before deployment today.

Where we push depends on what we learn. If simulation covers a strong majority of edge
cases, we push on **making it easy to reproduce environments in simulation.** If not, we
push on **making it easy to reset environments by remotely controlling the robot.**

## Why it matters

Evals are the feedback loop for the whole training stack. At 10 rollouts a 5-point gain is
noise; at 100 you can see it. **Bigger, faster, less noisy evals let teams detect smaller
deltas and converge faster.** That's the bet: more samples → better insight → better
ideation.

Looking at the loop, evals are **one of the last physical steps that can't yet be automated
in software.** Closing that loop lets robotics iterate far faster.

## Where it matters most today

**A) The improve/test cycle.** Someone scraps a policy together and it works → they chase a
customer → they hit edge cases → they fall into an improve/test/improve/test cycle. That's
where evals start to matter and teams reach for technicians. Pressure from a customer makes
companies increasingly sensitive to slight deviations in performance — exactly the small
deltas that small eval sets can't see. **This is where we come in.**

**B) Data quality analysis.** Egocentric/teleop data companies are everywhere; labs want to
scale this data but don't know how good it is. Proxies aside, the real test is to **train on
it and evaluate the policy** — painful because of (1) retraining cost and (2) eval cost.
**We cut the eval cost**, so dataset decisions rest on real performance, not guesses.

## Open challenges

_To be filled in from real customer conversations, not speculation._
