---
title: "Q&A Week 12"
date: 2022-04-13
---

This covers both the RL unit and Human-Centered AI part 1.

## RL

### Different Approaches to RL

Main difference is what functions we learn:

- *Policy*: Given a state, output (a distribution over) actions
- *Value*: Given a state, output an *expected return*
  - Common special case: *Q*: given a state *and an action*, output expected return
- *Model*: Given a state and an action, output a likely next state.
- new approach (Transformers-based): *Trajectory*: given a partial sequence of events (states, actions, and rewards), complete it.
  - Often we start with a *command* -- what got achieved (if anything) at the end of the trajectory.

### What's the "loss" (or target) in RL?

That's what makes it hard! e.g,. in Q-learning we try to minimize the *temporal difference*: how much the reward we get differs from the reward we predict (by subtracting the next-state value function from the current-state value function). But that's a difference of two predictions; if we were wrong, which of those two predictions was wrong?

In general, we're hoping to learn something about all possible things that could happen and things we could do, given data about only a fraction of what happened and things we did.

### Relationship to planning (e.g., minimax, Monte Carlo Tree Search)

They're good at different things:

- Classical planning algorithms:
  - How to *search* among possible action sequences?
  - Hard because of combinatorial explosion of possibilities.
  - Made practical by heuristic values about individual states and actions
  - Includes techniques like Beam Search
- Learned RL algorithms:
  - How to compute things about individual states and actions.
  - Hard because we only get data about a few of all possible trajectories.
  - Made practical by approximations.

So, unsurprisingly, the state of the art often combines both! See, e.g., MuZero.

### Can an agent trained in simulation be trusted in the real world?

Hm. Pro:

- We can set up things happening in the simulation that would be very rare or dangerous in the real world (e.g,. get an autonomous car to optimally reduce damage in a multi-vehicle collision in icy weather).
- We can get a lot more data about how the agent behaves.

Con:

- The simulation may not represent events that actually do happen, because the engineers never thought to program in a [building with a tunnel painted on the side](https://www.roadsideamerica.com/tip/4602).
- The agent may learn to exploit quirks in the simulator.

### Do human newborns learn by RL?

Maybe somewhat, but not really:

- RL is mostly about extrinsic motivation. Humans seem to have lots of intrinsic motivation.
- RL usually studies agents in isolation (although that's starting to change), but human learning is highly social.
- RL usually works in environments that are much much simpler than the real world. e.g., the real world is richly multimodal.
- RL is only as good as the function approximators it's learning. Even the state-of-the-art are far less rich and capable than human learning.
- etc. And we haven't even started discussing consciousness, creativity, etc.

## Interpretable AI

### Why can we ever trust a model if we can't see how it's making its decisions?

We trust human doctors routinely, even though, despite decades of effort by cognitive scientists, we have very limited knowledge about the process by which people make their decisions.

### Is there always a trade-off between understandability and accuracy?

**No**.

- Interpretable models are easier to *debug*.
- Interpretable models sometimes show us problems with the training data.
- If the true, generalizable behavior is actually simple, an interpretable model may have better *inductive bias*.

So why are we only learning about this now? Good question... 

### What's CART?

The classic algorithm for learning decision trees.

## Other

### What's dropout?

- Randomly setting some activations to 0.
- Often helps models train by reducing overfitting (the model can't overly depend on one specific thing because that might get dropped out)

### How do you get bitwise determinism?

- Careful handling of random state (e.g., seed)
- Carefully write algorithms so everything happens in a deterministic order
- Carefully...
