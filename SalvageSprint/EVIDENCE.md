# Week 1 evidence

Keep this short. Bullet points, a small table and one diagram or code trace are enough. This is your checkpoint record, not an extra report. Replace the prompts as you work.

Name:
Exact Unity version:
Checkpoint commit / repository:
Current stage and anything unfinished:

## Initial prediction

Three observations the rival needs, including one it might not have:

Seeing a pickup across a gap proves / does not prove reachability because:

One question about NPC behaviour:

## One complete trace

Use one actual situation. Include the observation data, derived facts, selected task and reason, movement request/result, and how feedback affects a later decision. Identify the responsible code locations. A tiny state diagram can accompany this trace.

## Scenario record

| Scenario | Predicted result | Observed result and short evidence / remaining issue |
|---|---|---|
| Normal loop and restart | Survey, collect, bank, continue, finish, restart| Works like intended afaik|
| Carrying cargo | Return to base| Works like intended, besides when target is taken.|
| Hidden / remembered pickup | Place in memory when spotted, ignore hidden pickups that haven't been seen yet| |
| Target taken | Release target, target 2nd highest prio and pursue. Repeat if 2nd target taken as well.| Takes 2nd highest prio but gets stuck|
| Unreachable target | Ignore unreachable target| Locks on to the unreachable target and gets stuck|
| No usable pickup | Explore map and return to base if no found| Keeps exploring and never returns to base|

Supplied test result, with any added tests identified:
Live walkthrough checked by / recording link if used:

## One correction and one independent check

The original weakness and why it happened:
What I changed and why it addresses the cause:
My counterexample or experiment: prediction, observed result, and one limitation:

## Collaboration and help

People I discussed or playtested with:
Code, sources or substantive tools/AI assistance I used, and how I verified them:
If unfinished: what works, exact reproduction steps, and the help I need:
