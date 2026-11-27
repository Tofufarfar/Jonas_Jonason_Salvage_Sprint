# Week 1 evidence

Jonas

6000.3.26f1

Checkpoint commit / repository: 

Stage 5 done

## Initial prediction

### Three observations the rival needs, including one it might not have:

 - List of remembered scrap and their locations
 - Check to not get into a locked state when unreachable target is being chosen
 - A way to tell if scrap is currently being held

### Seeing a pickup across a gap proves / does not prove reachability because:

It does not prove it. Line of sight is not a route, the pickup may or may not be reachable.

### One question about NPC behaviour:

Why does the Assasin's creed NPC lose track of the player when they crouch right next to them?

## One complete trace

Use one actual situation. Include the observation data, derived facts, selected task and reason, movement request/result, and how feedback affects a later decision. Identify the responsible code locations. A tiny state diagram can accompany this trace.

## Scenario record

| Scenario | Predicted result | Observed result and short evidence / remaining issue | Notes |
|---|---|---|---|
| Normal loop and restart | Survey, collect, bank, continue, finish, restart | Works like intended afaik | -|
| Carrying cargo | Return to base | Works like intended, besides when target is taken. (taken target hotfixed) | -|
| Hidden / remembered pickup | Place in memory when spotted, ignore hidden pickups that haven't been seen yet | Does not take remembered pickups into account | Correctly goes for the remembered scrap when it's the closest one|
| Target taken | Release target, target 2nd highest prio and pursue. Repeat if 2nd target taken as well. | Takes 2nd highest prio but gets stuck (taken target hotfixed) | -|
| Unreachable target | Ignore unreachable target | Locks on to the unreachable target and gets stuck | Temporarily ignores the unreachable target and surveys / goes to collect closest scrap|
| No usable pickup | Explore map | Keeps exploring and never returns to base | -|



### Supplied test result, with any added tests identified:
22 / 22

### Live walkthrough checked by / recording link if used:
Not used

## One correction and one independent check

### The original weakness and why it happened: 

Locks onto unreachable targets and does not proceed, because there was no check for the "candidate.Blocked" in the base code.

Another weakness was that remembered scrap got ignored, because there was no check for "candidate.Remembered"

### What I changed and why it addresses the cause:

Added the check for "IsEligble" where I check if the candicate is Visible or Remembered (as well as the check if it's Blocked). I intitially didn't use the helper method "IsEligble" because I didn't see the reason for it and because I had accidently completed Stage 2 & 4 before Stage 3.

I wasn't entirely sure how to solve Stage 3 on my own but it makes sense to iterate through the Candidates in Observeration to check for Remembered Id's. Then we only proceed if there are no Remembered && IsEligble targets.

### My counterexample or experiment: prediction, observed result, and one limitation:

I intially tried this code to skip Blocked and not Remembered candidates.

```
if (candidate.Blocked && !candidate.Remembered)  
{  
  continue;  
}
```
I falsely assumed that Blocked meant not Visible, which I was confused as to why there was two different variables. I then learned that the Blocked actually means Unreachable, so I decided to change the variablename.

## Collaboration and help

### People I discussed or playtested with:

Felix J, Teodora, Alexander

### Code, sources or substantive tools/AI assistance I used, and how I verified them:
CJ's Lectures
