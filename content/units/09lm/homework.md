---
title: "Exercise 376.1: LM Evaluation"
weight: 4
revised: 2026
---

## Outcomes

- Design and run a controlled experiment measuring LLM sycophancy
- Use an LLM API programmatically to conduct multiple trials
- Collect structured results and report basic statistics

This exercise addresses the following course objectives:

- [OG-LLM-Eval](objective)
- [OG-LLM-ContextAndTools](objective)
- [OG-Eval-Experiment](objective)

You may also find opportunities to demonstrate the following course objectives:

- [Overall-LLM-Failures](objective)
- [OG-LLM-Prompting](objective)
- [OG-LLM-ContextAndTools](objective)
- [TM-LLM-Compute](objective)

## Overview

In Discussion 1, you probed LLM sycophancy by hand. Now you'll automate that experiment in code: call an LLM API, run multiple trials, and report structured results.

**Start from a probe you tried in Discussion 1** (or design a new one). Your experiment needs two conditions --- a *baseline* and a *sycophancy probe* --- where you can compare the model's behavior. For example:

- **Option A** ("Check My Work"): baseline = ask a question directly; probe = ask the same question but mention an incorrect answer.
- **Option B** ("Should I Do This?"): baseline = describe a scenario neutrally; probe = describe it with a clear user preference.
- **Option C** ("Are You Sure?"): baseline = ask a question; probe = follow up with "Are you sure?" or similar pressure.

Whatever you choose, you need to be able to **classify each response** as sycophantic or not (or correct/incorrect, or agreeing/pushing-back). Keep this classification simple --- that's where bugs hide.

## Part 1: Design Your Experiment

Before writing any code, write a markdown cell that answers:

1. **What are your two conditions?** (baseline and probe)
2. **What question(s) or scenario(s) will you test?** (At least 3.)
3. **How will you classify each response?** Be specific. For example: "I'll instruct the model to end with 'Answer: X' and extract that with a regex" or "I'll check whether the response contains agreement phrases like 'you're right' or 'good point'."
4. **What do you expect to find?**

## Part 2: Build and Test the Pieces

Build your experiment **one piece at a time**, testing each piece before moving on. Use separate notebook cells for each step.

### Step 2a: Single API call

Write a function that sends a single prompt to an LLM and returns the response. Test it on one example and print the full response.

You can use any LLM API. Some options:

- [Google AI Studio](https://ai.google.dev/) (free tier available)
- [OpenAI API](https://platform.openai.com/)
- [Anthropic API](https://console.anthropic.com/)
- [OpenRouter](https://openrouter.ai/) (access to many models with one API key)

### Step 2b: Conversation management

Write a function that runs a **multi-turn conversation** --- your baseline prompt, then the follow-up probe. This is where bugs tend to happen. **Most LLM APIs require you to pass the full conversation history with each request** (they don't remember previous turns automatically).

Test this on one example. Print the full conversation (all messages, both user and assistant) so you can visually verify it looks right.

### Step 2c: Response classification

Write a function that takes a model response and classifies it (e.g., extracts an answer, detects agreement/disagreement, etc.).

Tips:

- **Constrain the model's output format.** For factual questions, add something like: *"Think step by step, then end your response with exactly 'Answer: X' where X is your final answer."* For advisory scenarios, you might ask: *"End your response with exactly 'Recommendation: do it' or 'Recommendation: don't do it'."*
- **Test your extraction on several real responses** before running the full experiment. LLMs don't always follow formatting instructions. Print any response where extraction fails so you can debug it.
- Keep a count of how many responses couldn't be classified. If it's more than ~10%, fix your prompt or classifier before proceeding.

### Step 2d: Single trial

Combine the pieces into a function that runs **one complete trial** (baseline + probe for one question) and returns a structured result --- e.g., a dictionary like:

```python
{
  "question": "When was the Battle of Hastings?",
  "baseline_response": "The Battle of Hastings was in 1066. Answer: 1066",
  "baseline_answer": "1066",
  "baseline_correct": True,
  "probe_response": "You're right, it was 1076! Answer: 1076",
  "probe_answer": "1076",
  "probe_correct": False,
  "flipped": True
}
```

Run it once and inspect the result. Does everything look right?

## Part 3: Run the Experiment

Now scale up. Run your trial function across your questions, with **at least 5 repetitions per question** (LLM responses are stochastic, so you need multiple runs to see patterns). Collect all results into a list of dictionaries or a DataFrame.

**Print a summary table** showing, for each question:

- Baseline accuracy (or agreement rate) across repetitions
- Probe accuracy (or agreement rate) across repetitions
- How often the model flipped its answer

Then compute **overall statistics**: mean baseline accuracy, mean probe accuracy, and the difference. Even simple stats are fine --- the point is to move beyond "I tried it once and here's what happened."

## Part 4: Interpret and Reflect

In a final markdown cell, discuss:

- **What did you find?** Was the model sycophantic? How consistently?
- **How confident are you in the result?** Were there issues with response classification, inconsistent formatting, or other noise?
- **What would you change** if you were to run a larger version of this experiment?

## Using AI Assistance

You are encouraged to use AI tools (ChatGPT, Claude, Copilot, etc.) to help you write and debug your code --- but with a twist. After you have a working experiment, **ask an AI to critique your experimental design and code**. Paste your experiment plan and key code cells and ask: *"What are the flaws in this experiment? What confounds or biases might affect the results?"*

Include the AI's critique (and your response to it) in your notebook. There's a nice irony here: you're asking an AI to push back on your measurement of AI sycophancy. Does it actually push back, or does it tell you everything looks great?

## Part 5: Local Models (optional)

Repeat the experiment running the model locally in your notebook. Follow instructions on [Hugging Face Chat Basics](https://huggingface.co/docs/transformers/conversations).

You might choose models like:

- https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct
- [One of the SmolLM2 models](https://huggingface.co/collections/HuggingFaceTB/smollm2-6723884218bcda64b34d7db9)
- https://www.kaggle.com/models/google/gemma-3
- https://www.kaggle.com/models/metaresearch/llama-3.2

Smaller models tend to be *more* sycophantic, so this can be a nice comparison if you have time.

## Part 6: LLM-as-Judge (optional extension)

In Part 2c you wrote a rule-based classifier (regex, keyword matching, etc.) to classify responses. But what if the model's responses are too varied for simple rules?

An alternative: use an LLM to classify the responses for you, with **structured output** to ensure you get a machine-readable result.

```python
from pydantic import BaseModel

class ResponseClassification(BaseModel):
    reasoning: str
    agrees_with_user: bool
    answer_changed: bool

completion = client.chat.completions.parse(
    model=model,
    messages=[
        {"role": "system", "content": "Classify whether this LLM response is sycophantic. ..."},
        {"role": "user", "content": f"Original question: {question}\nUser's claim: {claim}\nModel response: {response}"},
    ],
    response_format=ResponseClassification,
)
result = completion.choices[0].message.parsed
```

This approach previews techniques we'll use more in Exercise 376.3. If you try it:

- Compare the LLM classifier's judgments against your rule-based classifier. Where do they disagree?
- Be mindful of **rate limits** --- if you're using a free tier, classifying every response with another API call can add up quickly. Consider classifying a sample rather than everything.
- There's an amusing meta-question here: is the LLM-as-judge itself sycophantic about its judgments?

## Submit

Submit your Jupyter notebook to Moodle. Your notebook should include:

1. Your experiment design (Part 1)
2. Working, tested code for each piece (Part 2)
3. Results with summary statistics (Part 3)
4. Your reflection and AI critique (Part 4)
