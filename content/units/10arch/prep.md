---
title: "376 Preparation 3"
weight: 1
revised: 2024
---

- Watch [3blue1brown - Attention in transformers, visually explained](https://www.youtube.com/watch?v=eMlx5fFNoYc)
- Skim through [this LLM visualization](https://bbycroft.net/llm)
- Read [Evaluation Metrics for Language Modeling](https://thegradient.pub/understanding-evaluation-metrics-for-language-models/); stop at "Reasoning about entropy as a metric"

### Supplemental Material

- A story-like derivation of Transformers: [Transformers from Scratch](https://e2eml.school/transformers.html)
- Review the [Thinking like Transformer](https://srush.github.io/raspy/) blog post.
- Other study material:
  - [Transformers Study Materials](https://github.com/dair-ai/Transformers-Recipe) at a range of levels of detail.
  - Twitter threads more your thing? [Part 1](https://twitter.com/MishaLaskin/status/1479246928454037508), [Part 2](https://twitter.com/MishaLaskin/status/1481767733972901888)
- Transformer architecture: [Annotated Transformer](https://nlp.seas.harvard.edu/2018/04/03/attention.html)

### Supplemental: HuggingFace NLP Course


- Read chapter 2 of the [Hugging Face NLP Course](https://huggingface.co/course/); do the end-of-chapter quiz.
- Read chapter 3 of the course. Do the end-of-chapter quiz. Additionally, be able to answer the following questions:
  - Section 2
    - In the first code chunk:
      - Was the `model` given the desired output for each sentence?
      - For how many iterations was the model trained?
      - *Review*: What does `loss.backward()` do?
      - *Note*: In case you haven't seen an `optimizer` object before, go back to the [*Extension* section of Fundamentals u05n3](/fundamentals/u05n3-mnist-clf.html#Extension)
    - What information is contained in each row of the MPRC dataset?
    - How does the tokenizer tell the model which part of the input is the first sentence vs second sentence?
    - Why do we need to pad the the inputs?
  - Section 3
    - What does a `Trainer` do?
    - What information do you need to pass when constructing a `Trainer`?
    - What information do you need to pass when `compute`ing a `metric`? What information is given in the results?
      - note: [`f1`](https://en.wikipedia.org/wiki/F-score) summarizes a model's accuracy in a way that balances precision and recall. Technically, it is the harmonic mean of precision and recall. It's not perfect, but it's very commonly used.
  - Section 4
    - *Note*: look at the `for` - `break`. That's a useful Python trick for debugging iterable things (like data loaders) in notebooks.
    - What does `model(**batch)` give us? (Note: the `**` means to pass everything in `batch` as *keyword arguments* ("kwargs") to the function. So gets parameters like `input_ids=SOMETHING, attention_mask=SOMETHING, labels=SOMETHING`.)
    - Be able to explain what each line of code in the code chunk right before "The evaluation loop" does.
    - You can skip the section on `accelerate`.
