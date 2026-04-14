---
title: "Choosing a Project"
---

Pick a project where you can:

- Get something simple working quickly, then extend it
- **Measure something** — and then ask whether your measurement actually answers your question
- Write clearly about what you're doing and why
- Have fun!

## Structured Projects

These are well-defined starting points with external scaffolding, so you can spend your energy going deep rather than scoping.

### Best Model Under Constraints

Can you train the best language model possible on our lab machines (16GB GPU)? You'd adapt the ideas from the [NanoGPT speedrun](https://github.com/karpathy/nanochat) and [slowrun](https://github.com/qlabs-eng/slowrun) projects — which optimize for speed or data efficiency on large clusters — to a resource-constrained setting.

Some variants:
- **Best general LM** trained on lab hardware in under a day
- **Best translation model** for a specific language pair
- **Best coding agent** — see [nanocode](https://github.com/salmanmohammadi/nanocode/discussions/1) ([discussed here](https://news.ycombinator.com/item?id=47649742))

Good for demonstrating: transformer architecture understanding, training mechanics, experiment design, evaluation of generative models.

**Deepening ideas**: systematic ablations of architectural choices; analyze failure modes on a curated eval set; compare to a baseline API call.

### Kaggle Competition

Compete in an [active Kaggle competition](https://www.kaggle.com/competitions). Choose one that uses concepts from this class (NLP, vision, sequences).

Getting a baseline working is the easy part. Here's how to go deeper:

- Analyze **errors** systematically: what kinds of examples does the model fail on, and why?
- **Compare approaches**: at least two meaningfully different methods, with analysis of why one worked better
- Critique the **metric**: does the leaderboard score actually measure what the competition cares about?
- Discuss what you'd do with more compute, more data, or more time

## Open-Ended Projects

### Replicate or Extend a Paper

Pick a paper with a specific quantitative result and try to get the same number — then extend it.

Recent papers that are tractable and interesting:

- [s1: Simple test-time scaling](https://arxiv.org/abs/2501.19393) — just the "Wait..." prompting part, not the fine-tuning
- [Recitation over Reasoning](https://arxiv.org/abs/2504.00509) — when do LLMs fail at simple reasoning?
- [Cognitive Behaviors that Enable Self-Improving Reasoners](https://arxiv.org/abs/2503.01307) — focus on measurement and prompting, skip the RL
- [Blabrecs: a nonsense-word game](https://mkremins.github.io/blabrecs/) — fun, creative, tractable
- [Do Androids Laugh at Electric Sheep?](https://aclanthology.org/2023.acl-long.41.pdf) — humor understanding benchmarks
- [Prompting with Phonemes](https://arxiv.org/abs/2411.02398) — multilingual LLMs

Ask if you want suggestions tailored to your interests.

{{% details summary="Tips for replication projects" %}}

Before you start, verify:
1. Is there a specific quantitative result I can use as my anchor?
2. Can I access the same data, on hardware I have?
3. Do I understand the basic approach well enough to implement a simple version?

**The Benjamin Franklin method**: Read the original, take notes in human language. Close it, try to reimplement from your notes. Fail. Open it again. Repeat.

{{% /details %}}

### Build Something with LLMs

Build an application, evaluate it, and analyze its failure modes.

Some ideas:
- Search across multiple document sources (Google Drive, OneDrive, local files)
- Evaluate whether prompting strategies reduce LLM cognitive biases (sycophancy, hallucination)
- Analyze a large text corpus using LLMs (e.g., [Podcast Vibes](https://observablehq.com/@yurivish/podcast-vibes) style)
- [Build Your Own Timeline Algorithm](https://huggingface.co/blog/mozilla-ai/build-your-own-timeline-algorithm)

For any "build something" project: don't just show it works — measure where it fails.

### Extend Something from Class

Take any notebook from class and go deeper. Systematic extension with clear analysis is a completely valid project. Some weeks already have "Extension" suggestions.

## Deepening Any Project: Lenses to Apply

These aren't project types — they're ways to make any project stronger.

### Interpretability lens

Don't just measure what the model outputs — probe *why* it does what it does.

- Visualize attention patterns: what is the model "looking at"?
- Compare representations at different layers using probing classifiers
- Find examples where the model fails in revealing ways and trace back through the architecture
- Tools: [TransformerLens](https://github.com/TransformerLensOrg/TransformerLens), activation patching

**Behavioral probing** is a lightweight version: instead of looking inside the model, design inputs that reveal what the model can and can't do. For example: can it spell a word? Say each word twice? Alliterate? These connect directly to the tokenization topic — what does the model even "see" at the character level? Related paper: [Knowledge of Pretrained LMs on Surface Information of Tokens](https://arxiv.org/abs/2402.09808).

### Evaluation lens

For any number you report, also ask: *does this number actually answer the question we care about?*

- Compare quantitative metrics to qualitative inspection of outputs — do they agree?
- Test on distribution-shifted examples: does performance hold?
- What would a user actually care about, and how well does your metric proxy for that?
