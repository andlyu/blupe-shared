# Owl Evals

**Overnight robot-policy evals. Scored results by morning.**

## What it is

Owl is an overnight robot-policy evaluation service. You host the rig and define the task; Owl runs 10x the rollouts unmanned, using simulation plus remote teleop with automated scene resets and safety supervision. You wake up to scored, structured eval results (success rates, per-task breakdowns, failure modes, and regressions vs. your last checkpoint) by morning.

## The problem

Evaluating a robot policy means a human babysitting every rollout: run it, reset the scene, watch for safety, score it by hand. So teams run 30 evals instead of 300, and at that size a real improvement is indistinguishable from noise. Who feels it most: the robot-learning researcher who just changed the training recipe or added a small amount of ego-centric data and can't answer "did it actually work?", and the operator burning whole days resetting the bench. The people closest to making the policy better are throttled by the cost of finding out whether it got better.

## Who it's for

Robotics companies close to deployment, fighting tight customer requirements and a steady stream of edge cases. The day-to-day user is the robot-learning engineer who needs to know what data matters to their policy, whether the sensors or camera placement are limiting, and whether better labeling helps. Not academics running 30 rollouts for a paper.
