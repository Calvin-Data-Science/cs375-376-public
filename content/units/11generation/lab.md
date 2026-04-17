---
title: "Lab 376.4: Dialogue Agents, Prompt Engineering, Retrieval-Augmented Generation, and Tool Use"
weight: 4
revised: 2026
---

If under the hood all a language model does is predict the next token, how can you get it to do useful tasks for you? The key idea is to make "doing a task" look like "predicting the next token" in some context. This lab will introduce you to a few ways to do that.

We'll be using Qwen2.5-0.5B — the same Alibaba-released model whose dimensions (d=896, 14 attention heads) you worked out on the [Apr 10 Self-Attention Shapes handout](/handouts/2026_04_10.pdf) and loaded in {{% notebook name="Tokenization" nbname="u08n1-tokenization.ipynb" %}}. Today we'll compare its *base* version against its *instruction-tuned* version (`-Instruct`) to see what post-training actually changes.

## Objectives

- Describe how "few-shot learning" can be helpful for getting a language model to do what you want.
- Describe how a causal language model can be used to power a dialog agent.
- Explain how "chain of thought" prompting helps a model reason better.
- Explain how "tool use" works in language models.

This lab will address the following course objectives:

- [OG-LLM-APIs](objective)
- [OG-LLM-Prompting](objective)
- [OG-LLM-ContextAndTools](objective)
- [OG-LLM-Train](objective) *(base vs instruction-tuned comparison)*

You may also use this lab to demonstrate the following course objectives (e.g., by adding additional discussion to your notebook submission or having a conversation with the instructor or a chatbot):

- [TM-LLM-Generation](objective)
- [TM-LLM-Compute](objective)
- [OG-LLM-Tokenization](objective)
- [Overall-LLM-Failures](objective)
- [OG-LLM-Eval](objective)

## Getting Started

Start with the Lab 4 notebook. Also open a document where you can write the answers to the questions (we won't be turning in a notebook for this lab). **Create headings for each section of the lab** and write your answers under each heading.

{{% notebook name="Prompt Engineering" nbname="u11n1-prompt-engineering.ipynb" %}}

We'll use two different models: first, the non-instruction-tuned **base** model (`Qwen/Qwen2.5-0.5B`), then the instruction-tuned sibling (`Qwen/Qwen2.5-0.5B-Instruct`). Both are public on Hugging Face — no license acceptance needed. The 0.5B size fits comfortably on the free Kaggle/Colab GPUs.

## Base Model Warm-Up

Try completing the following tasks using the Qwen2.5-0.5B **base** model (without instruction tuning). Do this by modifying the `doc` given in the example code chunk. You might try setting the `do_sample` parameter to `True` (to get a sense of the range of possible outputs), or `False` (to get a single prediction).

1. A trivia task, like: "The capital of France is"
2. A math task, like: "2 + 2 = ___." (You might want to frame it like "Expression: 2 + 2. Result:")
3. A translation task, like: "An expert Spanish translation of 'Language models are statistical models that can generate text.' is ___."
4. A programming task, like:

```python
def sum_evens(lst):
  # Input: a list of numbers
  # Output: the sum of the even numbers in the list
```

{{% task %}}
1. Write a brief summary of how the base Qwen2.5-0.5B model performed on each task.
2. Notice that we expressed these tasks in the form of making reasonable completions of a document, not giving instructions to the model. What implications does this have for how useful the completion is?
3. Notice that the model took some time to generate the first token, then generated the rest of the text more quickly (but still not instantly). Given what you know about the Transformer architecture, what operations might be happening during this time?
{{% /task %}}

## Prompt Engineering

### Few-Shot Learning

In machine learning jargon, "shot" refers to the number of examples you have of a particular task. "Few-shot learning" refers to the problem of learning a new task with only a few examples.

For example, you might have noticed that the base model completes "The capital of France is" as if it were a travel article (or perhaps a multiple-choice question)---because that's the sort of document it was trained on! But you can give it examples of the sort of things you want. For example, try this instead:

```
The capital of Michigan is Lansing.
The capital of England is London.
The capital of France is
```

We can consider the first two lines as "examples" of the task we want the model to do. This is a "few-shot" example, because we're giving the model only a few examples of the task we want it to do.

Write a brief summary of how the base model performed on this task, as compared with not giving it any examples.

Also try this:

```
Request: capital("Michigan")
Response: "Lansing"
Request: capital("England")
Response: "London"
Request: capital("France")
Response:
```

### Chain of Thought

Try the following prompt, again with the base model:

```
I went to the market and bought 10 apples. I gave 2 apples to the neighbor and 2 to the repairman. I then went and bought 5 more apples and ate 1. How many apples did I remain with?
```

(Before you run this, think about how you would solve this problem.)

What does the model predict?

Now, add the following to the prompt: `Let's think step by step. After I bought the apples, I had`

How does the generated text change?

## Instruction Tuning

Instruction tuning does several things to make the model more useful at following tasks:

1. An instruction can get the model into the right "mode" for a task, more efficiently and reliably than few-shot examples can. For example, an instruction-tuned model will interpret questions like "What is the capital of France?" as a question, not as a continuation of a travel article.
2. Instruction tuning is also often done together with human feedback. Since the model was trained on the Internet, its training data includes both helpful and unhelpful examples, but the human feedback tunes the model to give the most helpful responses.
3. Instruction tuning gets the model to play the role of a dialogue agent, which is often a useful way to interact with a model.

Let's switch to the instruction-tuned model.

Change `USE_INSTRUCTION_TUNED = False` to `True` in the model loading cell of the notebook and re-run it. (You may want to restart the session first to free GPU memory.)

### Conversations as Documents

Instruction-tuned models were fine-tuned on documents formatted as dialogues between a user and an assistant. To get the best performance from these models at inference, we need to format our prompts in a similar way as the documents were formatted during fine-tuning. Different models have different fine-tuning formats, but fortunately the HuggingFace Transformers library has code to help us format our prompts correctly for each model.

The "Chat Templating" section of the notebook includes code to format the prompt for the instruction-tuned model. The `apply_chat_template` method takes a list of messages, where each message is a dictionary with two keys: "role" and "content". The "role" key can be either "user", "assistant", or "system". The "content" key is the text of the message.

```python
role = """You are a helpful 2nd-grade teacher. Help a 2nd grader to answer questions in a short and clear manner."""
task = """Explain why the sky is blue"""

messages = [
    {
        "role": "user",
        "content": f"{role}\n\n{task}",
    },
 ]
tokenized_chat = tokenizer.apply_chat_template(messages, tokenize=True, add_generation_prompt=True, return_tensors="pt")
print(tokenizer.decode(tokenized_chat[0]))
```

{{% task %}}
1. Describe how the model delimits user text and assistant text in the formatted prompt.
2. Describe how a model trained to predict the next token would generate an assistant's response to the question when given this prompt.
3. Use the model's `generate` method to generate a completion of this prompt. What does the model predict? (Refer to how we used the `generate` method in the earlier section)
{{% /task %}}

- Qwen2.5 chat template: https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct?chat_template=default
- Qwen2.5 tech report: https://arxiv.org/abs/2412.15115
- HuggingFace chat templating: https://huggingface.co/docs/transformers/main/en/chat_templating

### Retrieval-Augmented Generation

Completing a task often requires information that was not included in a model's training set. For example, try asking the following question to the instruction-tuned model (either omit the `{role}` or use a role like "You are an expert in PyTorch"):

"Explain the options for TripletMarginLoss in PyTorch."

Notice that the result includes *hallucinations*, i.e., information that it simply made up. This is a common problem with language models.

One way to reduce (**but not eliminate**) hallucinations is to explicitly provide the model with the information it needs. This is called retrieval-augmented generation. The idea is to provide the model with a "retrieval" of relevant information, which it can then use to generate a response.

> Note: I'd wanted to revise this exercise but ran out of time. I was going to have you ask it to give you suggestions for what courses to take at Calvin -- with and without revelant sections of the course catalog as context, and compare the results. For now, just do the PyTorch example. The goal was to see that the model would confabulate plausible-sounding information with no connection to reality, but would be more accurate when given the relevant context. You can also try it with other questions and contexts of your choice.

We'll use the docstrings for PyTorch functions as our knowledge base. Use the following code to extract the docstrings for all functions in the `torch.nn` module:

```python
import inspect

docstrings = {}
for name, obj in inspect.getmembers(torch.nn):
    if inspect.isfunction(obj) or inspect.isclass(obj):
        docstrings[name] = inspect.getdoc(obj)
```

Now, give the instruction-tuned model a prompt like:

```
{task}

Answer using the following context:
{context}
```

where `{task}` is the question you want to ask and `{context}` is the docstring for the function you want to ask about. In this example, use `context = docstrings['TripletMarginLoss']`. (Refer to the [documentation page](https://pytorch.org/docs/stable/generated/torch.nn.TripletMarginLoss.html#torch.nn.TripletMarginLoss) for the module to check the model's answer.)

{{% task %}}
1. Compare the truthfulness of the model's response with and without context.
2. We assumed that we'd given the model the exactly most relevant context. Try temporarily changing the model to use *all* of the docstrings: `'\n\n'.join(docstrings.values())`. Notice that you get an *error*: the context length was too big. **List two or three characteristics of the architecture and/or training of this model that may lead it to not be able to handle this much context.** (After receiving the error message, you might need to restart the session to continue using the model.)
3. Go back to using a single docstring, but make it the incorrect one (e.g., use `CrossEntropyLoss` instead of `TripletMarginLoss`). Compare the truthfulness of the model's response with the response given the correct context.
{{% /task %}}

> Note: In practice, we use a more sophisticated retrieval system, like a search engine, to provide the model with context. Often, *vector search* is used for the retrieval system: we find the document with the most similar vector to the prompt vector. Models like [Sentence Transformers](https://www.sbert.net/) are often used for this purpose, using models found on the Hugging Face model hub, such as [GTE](https://huggingface.co/thenlper/gte-large). See that model's documentation page for an example; you might try it out on your own.

### Tool Use

With RAG, *we* picked what context to give the model. A more flexible approach: let the model decide when it needs outside information and have it *emit a request* for that information — a structured call to a named function with arguments. That's a **tool call**.

Modern chat models like Qwen2.5-0.5B-Instruct are trained to emit tool calls in a specific format. The "Tool Use" section of the notebook walks through two stages:

1. **A simple demo**: the model emits a `<tool_call>` block for a weather lookup, but nothing executes it — you just see the structured output.
2. **A minimal agent loop** built cell by cell: build messages → apply chat template → generate → parse the `<tool_call>` output → dispatch → append tool result → loop. (HuggingFace documents a `tokenizer.parse_response` helper that would automate the parsing step, but it is not yet implemented for Qwen models, so the notebook shows the regex approach directly.)

**Wednesday**: complete the notebook through the end of the agent-loop walkthrough (before the "⚠️ Friday material" heading). Write answers for the tasks in the Base Model Warm-Up, Chat Templating, RAG, and Tool Use sections below.

## Friday

The "⚠️ Friday material" cells in the notebook give the agent a `run_bash` tool — real shell access to the Colab VM — and show what goes wrong in two scenarios:
   - **Scenario 1 — Prompt injection**: an "innocent" summarization task where the document being summarized contains instructions aimed at the model.
   - **Scenario 2 — Helpful cleanup**: an innocent-sounding request that the model might take too literally, potentially trashing the runtime environment.

These scenarios target the `OG-LLM-ContextAndTools` failure-diagnosis criterion. The planted secrets are all **fake** — the worst that can happen is you need to restart the Colab runtime.

Note: we could treat retrieval as a tool too. For example, the model could generate a request to run a search query against a database, then insert the results into the dialogue. This is called "agentic RAG".

We could also provide the model with other tools: a search engine, a call to an API like Wolfram Alpha (see [Stephen Wolfram's blog post on this topic](https://writings.stephenwolfram.com/2023/03/chatgpt-gets-its-wolfram-superpowers/)), or a call to an API that does something in the physical world (like turning on a light). Each additional capability multiplies the attack surface described in the scenarios above.

## Your Turn

Suppose we wanted to make a chatbot that answers incoming students' questions about Calvin University on topics like courses, schedule, recent events, activities, etc.

{{% task %}}
1. List a few specific questions that an incoming student might ask.
2. Describe how you would design a system that uses a language model to answer questions like these. **Refer to specific concepts introduced in this lab** or other prompt engineering concepts from the reading. Name at least one tool the system would need, and describe one failure mode from the scenarios above that applies.
{{% /task %}}

## Wrap-Up

Since we didn't need to write much code today, you don't need to submit a notebook. Instead, submit the answers to the tasks above.
