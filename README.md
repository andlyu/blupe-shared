# BluPe — Shared Ideas

A living doc for the high-level ideas we're working with at BluPe. Edit it, add to it,
disagree with it in line. This is the source of truth we think out loud in.

**How to work on this together:** clone the repo, edit `README.md` (or add files under
`ideas/`), commit, and push. Open a PR if you want eyes on a change before it lands.
History is the record of who changed what and why — write commit messages like notes to
the team.

---

## Current ideas for what BluPe is

These are working ideas, not settled conclusions. They'll change as we learn.

**Evals are a bottleneck for robotics.** Teams can't tell whether a change to their policy
actually helped without good eval signal, and good eval signal is exactly what's hard to
get. That bottleneck is what we're aiming to address.

**Evals have to be run in the real world.** A policy's real behavior shows up on real
hardware, in real scenes, under real variation — not only in simulation. So the eval
problem is fundamentally a physical-world problem.

**Running evals in the real world is itself a perfect application for robotics.** Real-world
evals mean executing rollouts, resetting scenes, and supervising safety over and over.
That's repetitive physical work in a controlled setting — exactly the kind of thing
robotics is good at. So we think the way to scale real-world robot evals is to bring
robotics (and automation) to bear on running them.

## Open questions

_Add yours. These are the things we don't have good answers to yet._

-
