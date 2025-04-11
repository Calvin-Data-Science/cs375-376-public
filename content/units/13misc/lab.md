---
title: "Lab: RL, Transformers, or other topics"
revised: 2024
---

Choose from one of the following notebooks, **or** do the Reinforcement Learning activities at the bottom of this page.

- {{% notebook name="Why so big? Counting parameters in sequence models" nbname="u13n1-count-params.ipynb" %}}
- {{% notebook name="Models for Sequence Data" nbname="u13n2-seq-models.ipynb" %}}
- {{% notebook name="Programming with Self-Attention" nbname="u13n3-self-attention.ipynb" %}}

## Reinforcement Learning

### Policy, Value, and Q functions

Go to the "Playground" at the bottom of [this article](https://distill.pub/2019/paths-perspective-on-value-learning/).

1. Change the Algorithm to Q-Learning. We won't look at the others at this time.
2. Try each of the "Visualization" options. What does each one show? Each one is a different function
3. Add one agent. How does completing an *episode* affect each of the functions that the agent is learning?

### Exploration

1. Set the Explore-Exploit slider all the way to Explore. What do you notice about the agent's behavior?
2. Set it all the way to Exploit. What do you notice now?

This environment isn't rich enough for exploration to help much. So: go to a different playground, where we can actually edit the environment and see what the agent learns.

[Observable RL Playground](https://observablehq.com/@kcarnold/q-table-reinforcement-learning)

1. Read through "Strategically Making Mistakes".
2. What does a low epsilon do? What does a high epsilon do?
3. Try editing the `maze = ` definition to edit the environment. What does it take to get the agent to tolerate a short-term negative reward to achieve a higher long-term reward?
