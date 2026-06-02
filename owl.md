# Owl Evals

**Overnight robot-policy evals. Scored results by morning.**

## Application

- **Full name:** Andrew Lyubovsky
- **Email:** a.l.andlyu@gmail.com
- **Affiliation:** The BluPe Project
- **Team:** Owl Evals · 2 people
- **Teammates:**
  - Andrew Lyubovsky — The BluPe Project
  - Shantanu Prakash — GSB
- **Build type:** both
- **Prototype:** in_progress
- **Referral:** Shantanu

## Product

Owl Evals

## Description

Owl is an overnight physical evaluation system for robot policies. Our first product, Owl Rig, is an eval-native teleoperation rig that sits around a customer’s existing robot workcell. The robot runs autonomously; Owl provides multi-view sensing, safety supervision, automated scene reset, and remote-assist teleop when the policy fails. The software layer schedules rollout batches, compares checkpoints, detects regressions, and produces structured eval reports by morning: success rates, time-to-completion, failure modes, intervention points, and examples of where the new policy improved or broke.

## Problem

Evaluating a robot policy means a human babysitting every rollout: run it, reset the scene, watch for safety, score it by hand. So teams run 30 evals instead of 300, and at that size a real improvement is indistinguishable from noise. Who feels it most: the robot-learning researcher who just changed the training recipe or added a small amount of ego-centric data and can't answer "did it actually work?", and the operator burning whole days resetting the bench. The people closest to making the policy better are throttled by the cost of finding out whether it got better.

## Who it's for

Robotics companies close to deployment, fighting tight customer requirements and a steady stream of edge cases. The day-to-day user is the robot-learning engineer who needs to know what data is important to their policy, whether there are limitations in the sensors or camera placement, and whether better data labeling helps. Not academics running 30 rollouts for a paper.
