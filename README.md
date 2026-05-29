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

## How teams get here

Someone scraps a policy together and it works → they chase a customer → they hit edge cases
→ they fall into an improve/test/improve/test cycle. That's where evals start to matter and
teams reach for technicians. **This is where we come in.**

## The approach: simulation + remote teleop

- **Simulation** to continuously validate the model's performance — rough signal that
  might not be 100% accurate, but cheap and always-on.
- **Real-world testing** once a policy is good enough, then **continuous testing in
  deployment.**

How far testing can move into sim is unclear, but labs test heavily in the real world
before deployment today. So the **short-term solution is remote teleop**: instead of a
technician beside the robot, the robot itself is driven remotely to reset the environment
between rollouts.

It's a **combination of simulation and remote teleop**, not just a teleop service.

## The eval flavor

Across both sim and teleop, the deliverable is a **research artifact, not a log of operator
time** — numbers, comparisons, and diagnostics that help the team understand how their
policy actually behaved:

1. **Report numbers** — success rate, per-task breakdowns, variance, regressions vs. prior
   checkpoints. A scorecard, not a video archive.
2. **Help researchers understand the policy** — surface and cluster failure modes, flag
   regressions. A debugging tool, not just a grade.
3. **Run designed eval sets** — deliberately vary lighting, distractors, and initial
   conditions so the numbers say something about generalization.

## Why it matters

Evals are the feedback loop for the whole training stack. At 10 rollouts a 5-point gain is
noise; at 100 you can see it. **Bigger, faster, less noisy evals let teams detect smaller
deltas and converge faster.** That's the bet: more samples → better insight → better
ideation.

## Second area: data quality analysis

Egocentric/teleop data companies are everywhere; labs want to scale this data but don't
know how good it is. Proxies aside, the real test is to **train on it and evaluate the
policy** — painful because of (A) retraining cost and (B) eval cost. **We cut the eval
cost**, so dataset decisions rest on real performance, not guesses.

## Open challenges

_To be filled in from real customer conversations, not speculation._
