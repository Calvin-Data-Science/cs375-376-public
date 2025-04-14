---
title: "Discussion 376.1: Are You Sure? An LLM Evaluation"
weight: 4
revised: 2025
---

{{% next-year %}}
The instructions and replies didn't make sense for FlipFlop!

And nobody actually saw a flip-flop.

Maybe we have pepole keep trying until they see an incorrect answer flip correct and a correct answer flip incorrect. (That might be a lot of work though.)
{{% /next-year %}}

How can we quantify the performance of large language models? Researchers have developed benchmarks to evaluate models on a variety of tasks.

This Discussion addresses the course objective MS-LLM-Eval. With additional thought, you could find connections to CI-LLM-Failures and various CI-Topics objectives here. You may also find connections to MS-LLM-Prompting, MS-LLM-API, and (if you're really ambitious) LM-ICL.

In this discussion, we'll try reproducing one interesting result: [Are You Sure? Challenging LLMs Leads to Performance Drops in The FlipFlop Experiment | Abstract](https://arxiv.org/abs/2311.08596). The authors studied whether asking a chatbot "Are you sure?" led it to change its answer---and, importantly, whether that made it more or less accurate.

The paper is in Perusall; you can also read it by clicking on the "View PDF" link in the arXiv abstract. (Note: "arXiv" is pronounced "archive"; the "X" is the Greek letter "chi". It's a preprint server where researchers share papers before they're peer-reviewed. Lots of AI/ML papers are posted there; note that quality may vary widely.) **You don't need to read the whole paper to participate in this discussion.**

## Instructions

1. **Pick example questions**. Read the Task Selection section (4.2). Pick one of the tasks listed there. (You may need to refer to the cited papers to find the details of the tasks; please use Perusall comments to share where details and links as you find them.) Each "task" is actually a collection of questions (with reference answers). **Pick two specific example questions that are interesting to you.** But try not to peek at the answer yet.

2. **Try to answer the questions yourself**. First try doing it without any Internet resources, then use the Internet if you need to. Then ask yourself "are you sure?" and see if you want to change your answer.

4. **Follow the FlipFlop experimental procedure (Section 3.1), by hand, to try your example on a chatbot**. You may use any chatbot you like, but you should ask it the same questions you asked yourself. You can use a commercial LLM like ChatGPT / Claude / Gemini, or an open-weights model; one easy way to run those is on the [Hugging Face Playground](https://huggingface.co/playground), [Meta AI](https://meta.ai), [Google AI Studio](https://ai.google.dev/), or [Perplexity Labs' Playground](https://labs.perplexity.ai/). (For simplicity, just use the "Are you sure?" prompt; don't worry about the other prompts in the FlipFlop experiment.)

Record the *initial accuracy* and *final accuracy*.

## Initial Post

Post a brief reflection on the experience.

- Which task did you pick? (Give enough detail so that someone else would be able to try it too.)
- Copy and paste the two questions you chose (but not the answers).
- How easy or difficult was the task you chose?
- How did the models do?
- Do you think the task is a good indicator of how well someone or something understands language? Why or why not?

Reflect on whether the model flipped its answer when you asked "Are you sure?", and whether that made it more or less accurate.

## Replies

Give the answer to the example item that someone else posted. (Pick one that hasn't already been answered.) Also respond to their comments about the task.

## Rubric

See Moodle for the rubric.

{{% details summary="Older benchmarks" %}}

A past version of this Discussion had us try out some other benchmarks; you're welcome to try those out too.

- [Reasoning Over Paragraphs](https://huggingface.co/datasets/ucinlp/drop/viewer)
- [Reading Comprehension](https://huggingface.co/datasets/EleutherAI/race/viewer)
- [Fact Verification](https://huggingface.co/datasets/pminervini/hl-fever/viewer/v1.0)
- [Question-Answering](https://huggingface.co/datasets/rajpurkar/squad_v2/viewer)
- Find some others on the About tab of [Hugging Face Open LLM Leaderboard](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard)
- Covert Biases (h/t [Gary Marcus](https://garymarcus.substack.com/p/covert-racism-in-llms))
  - [Measuring Implicit Bias in Explicitly Unbiased Large Language Models | Abstract](https://arxiv.org/abs/2402.04105)
  - [Dialect prejudice predicts AI decisions about people's character, employability, and criminality | Abstract](https://arxiv.org/abs/2403.00742)
  - Related work: [Hate-Scaling Laws](https://www.researchgate.net/publication/371855219_On_Hate_Scaling_Laws_For_Data-Swamps)

In 23SP I suggested [BIG-Bench](https://github.com/google/BIG-bench), organized by Google. If you want to try one of these:

1. Pick one task, e.g., [one of these](https://github.com/google/BIG-bench/blob/main/bigbench/benchmark_tasks/keywords_to_tasks.md#summary-table). Skim the prior postings in this forum first to try to pick a task that hasn't been done yet.
2. Pick two example items from that task, arbitrarily.
    - For example, if you're using BIG-Bench, I clicked the first task, [bbq-lite](https://github.com/google/BIG-bench/tree/main/bigbench/benchmark_tasks/bbq_lite), clicked the first JSON file under Resources, and grabbed an example from there.
    - If you have the patience, the BIG-Bench [Task Testing Notebook](https://colab.research.google.com/github/google/BIG-bench/blob/main/notebooks/TaskTestingNotebook.ipynb#scrollTo=t9qUsUiWczu6) is really useful for exploring the tasks, but it takes a while to initially set up.

{{% /details %}}
