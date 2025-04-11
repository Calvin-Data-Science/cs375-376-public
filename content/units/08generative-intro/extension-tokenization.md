---
title: "Optional Extension: Token Efficiency Analysis"
revised: 2025
---

This is an optional mini-project that builds on the tokenization exercise that we did this week.

1. Select 4-5 text samples (100-200 words each) from different domains. Examples include:

    - General prose (e.g., news article)
    - Code or structured data (e.g., HTML, JSON, XML, CSV, ...)
    - Technical/scientific text
    - Social media/informal text
    - Non-English or multilingual text

2. Select two or three tokenizers to compare (e.g., Llama, Gemma, spaCy, sklearn's TextVectorizer, etc.). You may use the same tokenizers from the previous exercise or try new ones.

3. For each tokenizer, tokenize the text samples and calculate the following metrics:

    - Characters-per-token ratio
    - 5 longest tokens
    - 5 multi-token words (if applicable)
    - 5 words mapped to an "unknown" token (if applicable)

4. Analyze the results and answer the following questions:

    - Which types of text tokenize most efficiently and why?
    - How might these insights influence prompt design for different tasks?
    - What specific improvements could be made to the tokenization process for one of your text domains?

