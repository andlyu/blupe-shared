# BluPe — Shared Ideas

A living doc for the high-level ideas we're working with at BluPe. Edit it, add to it,
disagree with it in line. This is the source of truth we think out loud in.

**How to work on this together:** clone the repo, edit `README.md` (or add files under
`ideas/`), commit, and push. Open a PR if you want eyes on a change before it lands.
History is the record of who changed what and why — write commit messages like notes to
the team.

---

## What BluPe is doing

Automate robot policy eval runs so teams can run them overnight and get **10x more
rollouts with more variation, without a person having to babysit each one.**

Today every rollout costs a local human's attention — running it, resetting the scene,
watching for safety, scoring the outcome. That caps how many evals a team can run and
pushes them toward small, hand-picked eval sets that don't really stress the policy.

The one-liner: **a remote teleop service with an eval flavor.** Generic remote teleop
just drives the robot. We do that, but the deliverable is a research artifact — numbers,
comparisons, and diagnostics — not a log of operator time.

## Who owns what

- **The team (customer) owns:** the robot, the workspace, the rig, the task definition,
  the policy.
- **We own:** rollout execution, environment resets, safety supervision, scoring,
  scheduling, diagnostics, and the dashboards/tooling our operators and their researchers
  use.

They leave the rig on overnight; we run rollouts against it; they get back **scored,
structured eval results** in the morning — not just video.

## The eval flavor — what makes us not just teleop

1. **Report numbers.** Success rate, per-task breakdowns, variance, comparisons against
   previous checkpoints. The output is a scorecard, not a video archive.
2. **Help researchers understand the policy.** Surface failure modes ("fails when the
   target is left of center"), cluster similar failures, flag regressions vs. the last run.
   The eval is a debugging tool, not just a grade.
3. **Run designed eval sets, not arbitrary tasks.** Scenario sampling with coverage in
   mind — vary lighting, distractors, initial conditions deliberately — so the numbers we
   hand back are actually informative about generalization.

## The thesis

**Larger sample sizes give researchers better insights — and better insights lead to
better ideation.** That's the whole bet. Researchers today iterate against eval sets too
small to tell signal from noise. An order of magnitude more rollouts, across more
variation, surfaces failure modes, regressions, and recipe wins that current eval volumes
hide. Sharper signal means sharper hypotheses about what to try next — which data to
collect, which recipe to tune, which architectural change is worth the compute.

## Why it matters now

- **Evals are the iteration bottleneck for the training stack.** Every data-mix decision,
  recipe change, and architecture experiment gets graded against an eval. Small, slow, or
  noisy evals mean teams iterate on muddy signal. This applies to every team training a
  policy, not just teams approaching deployment.
- **Small signals stay invisible without volume.** At 10 rollouts per task, a 5-point
  improvement is indistinguishable from noise. At 100, you can see it. The team that
  detects smaller deltas converges on the right recipe faster.
- **The local-human-in-the-loop is the binding constraint.** Teams don't run small eval
  sets because small is enough — they run small because a person has to be present for
  every rollout. Remove that constraint and test volume goes up an order of magnitude.

## Open questions

_Add yours. These are the things we don't have good answers to yet._

- What are the biggest real challenges? (To be filled from actual customer conversations,
  not speculation.)
-
