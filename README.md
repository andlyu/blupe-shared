# BluPe — Shared Ideas

A living doc for the high-level ideas we're working with at BluPe. Edit it, add to it,
disagree with it in line. This is the source of truth we think out loud in.

**How to work on this together:** clone the repo, edit `README.md` (or add files under
`ideas/`), commit, and push. Open a PR if you want eyes on a change before it lands.
History is the record of who changed what and why — write commit messages like notes to
the team.

---

# Automating Robot Policy Evals — Working Thesis

> Written in positions, not prose. Update as the thesis sharpens.

## What we're trying to do

Automate eval runs so people can run them overnight and get **10x more runs with more
variation, without a lab person having to babysit them.**

Today, most evals are done manually: a policy runs, and then the environment is reset, over
and over. Who does that work depends on the team's stage. **Smaller labs and companies have
researchers babysitting the rollouts** — the people building the policy are also the ones
resetting the scene. **Larger labs and companies, closer to production, have technicians**
doing it. Either way there's a physical person in the loop for every rollout.

That puts a hard ceiling on how many evals a team can run, and pushes them toward small,
hand-picked eval sets that don't actually stress the policy. **What we want is to take the
physical person out of that loop.**

The pitch in one line: **a remote teleop service, with an eval flavor.** Generic remote
teleop would just drive the robot. We do that, but the deliverable is a research artifact,
not a log of operator time: numbers, comparisons, and diagnostics that help the lab
understand how their policy actually behaved.

How it works: the lab owns the physical setup — they host the robot, build the rig, define
the task. We take over the operator role from there: our team runs the rollouts and resets
the environment between them, from a remote ops center, with as much automation in the
loop as we can build. The lab leaves the rig on overnight; we run rollouts against it; they
get back **scored, structured eval results** in the morning — not just video.

What we own vs. what the lab owns:
- **Lab owns:** the robot, the workspace, the rig, the task definition, the policy.
- **We own:** rollout execution, environment resets, safety supervision, scoring,
  scheduling, diagnostics, and the dashboards / tooling our operators and the researchers
  use.

## How we see the loop getting automated: simulation + remote teleop

We expect taking the person out of the loop to come from a **mix of simulation and remote
teleop**, used at different stages of the policy's life:

- **Simulation** to continuously track the policy's improvement. Cheap, fast, always-on
  signal as the policy trains.
- **Real-world testing** once a policy is good enough — and then **continuous testing in
  deployment** after that.

How good simulation gets, and how much of testing can actually move into sim, is still
unclear. What we do know: **labs today test heavily in the real world before deployment.**
That's not going away soon.

So the **short-term solution is remote teleop.** Instead of a technician sitting next to the
robot, the robot is controlled remotely to reset the environment between rollouts. Same
physical eval loop, minus the requirement that a person be physically present for it.

## The eval flavor — what makes us not just teleop

Three things we do that a generic teleop service wouldn't:
1. **Report numbers.** Success rate, per-task breakdowns, variance, comparisons against the
   lab's previous checkpoints. The output is a scorecard, not a video archive.
2. **Help researchers understand the policy.** Surface failure modes (e.g. "fails when the
   target is left of center," "drops the object on rotation > 30°"), cluster similar
   failures, flag regressions vs. the last run. The eval is a debugging tool, not just a
   grade.
3. **Run designed eval sets, not arbitrary tasks.** Scenario sampling with coverage in
   mind — vary lighting, distractors, initial conditions deliberately, so the numbers we
   hand back are actually informative about generalization.

The frame: **evals are the feedback loop for the entire training process.** What data to
collect next, how to tune the training recipe, whether the last change helped — all of
these decisions depend on eval signal. Bad evals (small sample, slow turnaround, noisy
scoring) mean teams iterate on muddy signal: they can't tell whether a recipe change
actually helped, so they over-rotate on noise or under-rotate on real wins. High-quality
evals catch smaller deltas, which compresses the iteration loop and lets teams push the
policy further per unit of time. As policies approach deployment, broader variability
coverage adds confidence on top of this — but only meaningfully for teams without a strong
human-in-the-loop safety net during deployment.

## Why this matters now

- **Evals are the iteration bottleneck for the training stack.** Every data-mix decision,
  every recipe change, every architecture experiment ultimately gets graded against an
  eval. If the eval is small, slow, or noisy, the team can't tell which changes helped — so
  they iterate on muddy signal, over-rotate on noise, and under-rotate on real wins. Bigger,
  faster, less noisy evals tighten the loop directly. This is the strongest reason it
  matters, and it applies to every team training a policy, not just teams approaching
  deployment.
- **Small signals stay invisible without volume.** At 10 rollouts per task, a recipe change
  that improves success rate by 5 points is indistinguishable from noise. At 100 rollouts,
  you can see it. The team that can detect smaller deltas converges on the right recipe
  faster — sometimes by an order of magnitude faster — than the team that can't.
- **Deployment raises the value of variability coverage — conditional on the safety net.**
  What pre-deployment testing actually buys a team is the ability to test across more
  variability (lighting, distractors, object configurations, edge conditions) and ship with
  higher confidence. If there's a human in the loop during deployment catching failures,
  that confidence is less load-bearing — the safety net is doing the work. If deployment is
  autonomous or supervision is thin, the confidence from broad pre-deployment testing is
  doing the work instead. Either way, it's a secondary argument to the iteration-speed one
  above; teams need good evals long before they get to the deployment conversation.
- The local-human-in-the-loop requirement is the binding constraint on how much testing
  actually happens. Teams aren't choosing to run small eval sets because they think small is
  enough — they're running small because a person has to be present for every rollout.
  Remove that constraint and test volume goes up by an order of magnitude.

## The thesis

**Larger sample sizes give researchers better insights — and better insights lead to better
ideation.** That's the whole bet. Today researchers iterate against eval sets too small to
distinguish signal from noise; running an order of magnitude more rollouts — across more
variation — surfaces failure modes, regressions, and recipe wins that current eval volumes
simply hide. Sharper signal means sharper hypotheses about what to try next: which data to
collect, which recipe to tune, which architectural change is worth the compute. Everything
we build serves that one outcome.

## Biggest challenges

_To be filled in based on actual customer conversations, not speculation._
