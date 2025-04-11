---
title: "Choosing a Project"
revised: 2025
---

Overall, pick a project where you can:

- Get something simple working quickly, then extend it
- **Measure something**: performance, interpretability, etc.
- Write clearly about what you're doing
- Think about the implications of what you're doing
- Have fun!

Here are some ideas to get you started:

## Replicate or Extend an Academic Paper

I often come across a paper that makes me think, "my students could have done that!" Here are a few examples:

- [Blabrecs: a nonsense-word game](https://mkremins.github.io/blabrecs/) ([the paper](https://mkremins.github.io/publications/Blabrecs_NeurIPS2023.pdf))
- [Knowledge of Pretrained Language Models on Surface Information of Tokens | Abstract](https://arxiv.org/abs/2402.09808)
- [s1: Simple test-time scaling | Abstract](https://arxiv.org/abs/2501.19393) (just do the "Wait..." part, not the fine-tuning)
- [MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents | Abstract](https://arxiv.org/abs/2404.10774) (either just do the dataset collection, or just do the fine-tuning)
- [Recitation over Reasoning: How Cutting-Edge Language Models Can Fail on Elementary School-Level Reasoning Problems? | Abstract](https://arxiv.org/abs/2504.00509)
- [Do Androids Laugh at Electric Sheep? Humor “Understanding” Benchmarks from The New Yorker Caption Contest](https://aclanthology.org/2023.acl-long.41.pdf)
- Update [alex-lew/robot-mind-meld: A little game powered by word vectors](https://github.com/alex-lew/robot-mind-meld) to work with modern LLMs
- [“Turning right”? An experimental study on the political value shift in large language models | Humanities and Social Sciences Communications](https://www.nature.com/articles/s41599-025-04465-z) - replicate?
- [Prompting with Phonemes: Enhancing LLMs' Multilinguality for Non-Latin Script Languages | Abstract](https://arxiv.org/abs/2411.02398)
- [Cognitive Behaviors that Enable Self-Improving Reasoners, or, Four Habits of Highly Effective STaRs | Abstract](https://arxiv.org/abs/2503.01307) (you can skip the RL part, focus on the measurement and prompting)

I have a whole collection of others; just chat with him about what you're interested in.


## BYOTA

I just saw this and it looks like a great project! [Build Your Own Timeline Algorithm: A Blueprint](https://huggingface.co/blog/mozilla-ai/build-your-own-timeline-algorithm)


## Prof Arnold's prototypes

- [Careful Translation Workflow](https://kenarnold.org/posts/translation-workflow/)
  - Evaluate it
  - Explore alternative approaches
    - Generate an editable scratchpad, with intermediate questions and tentative answers
    - Something like [HumanLayer](https://www.humanlayer.dev/)?
- Multilingual Chat: evaluate it, make it faster, make it actually useful for multilingual conversations; evaluate using voice LLMs for this task
- Predictive-Text for Assistant Response
- [Reflective Communication](https://kenarnold.org/posts/reflective-ai/)
  - Extend to allow teams to articulate what sort of feedback they want to get
- [Screen-Free Reflective Practice](https://kenarnold.org/posts/reflective-practice/): build an app for this?

## Extending anything from class

Take any notebook we do in class. Extend it in some way that's interesting to you, and write clearly about your experience. That's a totally valid mini-project. You might need to do a few of these to hit all of the objectives, but that's great. Some weeks already have "Extension" ideas.

## Working with LLM APIs

- Real-time presentation outliner ("I spaced out for a minute, what did I miss?")
- Say your team has big collections of documents… in two or more different systems (Google Drive, OneDrive, local computer, …). You're looking for something but don't know which system it's even in. Can we make a way to search across multiple different systems?
- Build an apologetics debate platform: prompt agents to take different positions on an issue specified by the user, generate a debate with each other, and allow the user to interject. Important: Also thoughtfully analyze whether we should do this.
- Use LLMs to analyze a bunch of text data. Example: [Podcast Vibes](https://observablehq.com/@yurivish/podcast-vibes).

- Evaluation
  
  - Are there prompting strategies that help LLMs avoid their cognitive biases (e.g., sycophany/agreeableness, hallucination, etc.)? Could the LLM proactively reason about how to avoid those problems, and/or retrospectively analyze its response and identify potential errors?
  - Do LLMs respond meaningfully differently when prompted with 2nd person language ("can you do this for me?") vs collaborative language ("can we do this together?" or "what if we…?")
- Which LLM libraries are vulnerable to token injection vulnerabilities, e.g., if the user message includes the representation of [special tokens](https://huggingface.co/docs/transformers/main/en/chat_templating) that mark system or assistant messages. See https://github.com/huggingface/tokenizers/issues/1458

## Working with Models Directly

- An idea: use a pretrained autoregressive model as if it were a diffusion LM by simply instructing it to "fill in the blanks" in a document (and then giving the blanked document as input)
- Music: chord progression variations, passing chords
  - how to link with melody?
- RL: Play with reward hacking


## Compete in a Competition

You may compete in a Kaggle competition or similar competition, like:

- [ARC Prize](https://arcprize.org/)
- [Humanity's Last Exam](https://lastexam.ai/)
- [Kaggle](https://www.kaggle.com/competitions)

If you do this, you should:

- Choose a competition that uses concepts from this class (e.g., NLP or computer vision). You can work with a partner if you like. You should aim to get a score that's competitive with the top 10% of the leaderboard. You should also write a report on your approach and results.
- Since you should be able to get a baseline approach working quickly (by referring to what other participants did), here are some ways you can deepen this kind of project:
  -   Analyze the model's **errors**, both quantitatively and qualitatively.
  -   **Compare several approaches.** You can consider differences in model architecture, specific task, hyperparameter choices, inclusion/exclusion criteria, etc. Remember to think about the choice of **metrics** and the **uncertainty** involved in any estimate of them.
  -   Generate **explanations** of the model's decisions, using the model interpretation methods described in the book or otherwise.
  -   Discuss how you were able to **tune** the performance of the model.

## Creativity

Use ML to empower human creativity in some way. For example, you might try to generate art, music, or poetry, or to help with the creative process in some other way.

For this project, you should aim for:

- Hacking something about the model or data, not just using something off-the-shelf
- Demonstrating some *creative output* (e.g., a generated image, poem, or song)
- Thinking through the *creative process* that led to that output

## Replication and/or Constraints

- Pick a single quantitative result from a research paper, blog post, etc. and try to replicate it. (*"They got a number. Can we get the same number?" (or better?)*)
- Write some part of the code yourselves (data input, modeling, optimizer, experiment harness, etc.)
- Then **extend** in some way.

One way you could extend a replication project is to add constraints: limited compute (e.g., lab computers, your laptop, Raspberry Pi), limited data (a small subset of the original dataset), limited model size (fits in xx MB), etc.

One example I'd really like to see: **Train the best language model you can on our lab computers** (or your laptop).

{{% details summary="Details on Replication Projects" %}}


### Expectations for Replication Projects

- For these projects, we will not expect as much discussion of motivation, assuming that the original artifact took care of that.
- Depending on your results, you should either:
  - Demonstrate *surmounting significant technical challenge* in attaining the result,
  - Provide a thoughtful *analysis* of the decisions you and the original authors made, or
  - Improve on the quantitative result in some measurable and well-motivated way.

### Choosing a Replication Project

If you're choosing a replication project, ask yourself:

1. Is there some specific write-up, with quantitative results clearly reported, that I can use to anchor the project?
2. Can I easily access the same data that the original authors used? (Does it fit on computing hardware I can easily access?)
3. Do I understand the basic approach? Maybe there's fancy stuff too, but you should be able to think of how you'd implement a simple version of it.

### Expository Notebooks ("Notebookify")

One strategy to take when starting with an existing code is to "Notebookify" it. Most notebooks you'll find are *demo* notebooks, designed to show off the best results but hide a lot of details behind opaque code chunks or external libraries. In contrast, an *expository* notebook **walks the reader through what's going on**.

The code part of such a project is relatively straightforward: find a demo notebook, step through it, pull in the contents of the "do-all-the-stuff" functions (test that it still works), split things up into individual cells (test that it still works), and show intermediate results and shapes. But you'll also write up descriptions of what's happening.

You will almost certainly want to refer to a paper by the original authors. It'll usually explain the names of variables and methods, and it'll show what parameters and data are likely to work well.

If the original has big loops, flatten them. For example, show one example of how the data is prepared, run one minibatch of the model training, show how the evaluation scores are computed for one datapoint.

Simplify the code as needed. e.g., if there are `if`s to do different things depending on configuration, remove the code that isn't actually run in your case.

Most importantly, explain what is going on. Start with an intro about the overall goal of the approach you're demoing, and the basic outline of what the process looks like. Then dive in. End with a conclusion summarizing the main points that you highlighted about what's going on. Perhaps end with some questions and future directions: what decisions did the original authors make that aren't clear to you? What ideas might you have for doing something differently?

### How to replicate without duplicating

One strategy: the Benjamin Franklin replication. Here's how I adapt it to code:

1. Read the original. Take notes in a separate document. Make them mostly in human language or math; put code in your notes only sparingly.
2. Close the original. Try to write a replication based on your notes.
3. Fail at some point because your notes aren't detailed enough. So **close your replication** and open the original again, and return to step 1.

### Tips for Replication Projects

Basic outline of a project here:

- Get the code running (could be very easy if you find a Colab notebook etc)
- Replicate something interesting that's already been done.
- Use an example that you provide instead of one of their pre-built ones.
- Push the limits a bit.

### Ideas of what to replicate

- Compete in https://babylm.github.io/ (train a language model on only data that a human child plausibly has access to).
  - Suggestion: initialize your model wisely.
- Train the best LM you can on a lab machine in under a day, on permissively licensed data and/or synthetic data.

See <https://paperswithcode.com/> for some examples. Their [newsletter](https://paperswithcode.com/newsletter) is particularly approachable.

Also, see proceedings of general conferences like NeurIPS, ICML, ICLR, ..., or domain-focused conferences: text (EMNLP, ACL), speech and music (ISMIR, InterSpeech), computer vision (ICCV, SIGGRAPH), recommender systems (RecSys), etc.

{{% /details %}}

## Teaching

Create materials to teach this class about a topic beyond the scope of the course.

Deliverables should include at least 3 of the following:

- Learning objectives (skills that students will have after the lesson, terms they will know, etc.)
- Lecture slides (with video narration)
- A demo notebook (with a video walkthrough)
- A hands-on lab activity (ideally with a video walkthrough)
- Several quiz questions
- A homework assignment (with example solutions)

Examples: [Jay Alammar's blog](https://jalammar.github.io/), many articles on [distill.pub](https://distill.pub/), [3Blue1Brown videos](https://www.youtube.com/c/3blue1brown), ...


## Other Project Ideas

  - Add details to image descriptions, ask questions, present some options
  - Unpack run-together words. For example, a truck drove by with "inontime" written on it; output "in on time".
  - Decompiler: given assembly or bytecode, generate the source code, including comments and variable names.
  - organizing personal info: given a block of text, figure out where it goes in an existing organization system
- **Mechanistic Interpretability**: Probe at how things work. [details](interpret/)
  - Can we identify the latent behaviors in language models? Can we factor the model into activating and then executing behaviors? Structure of soft prompts?
  - How does the model encode literal phrases of text? Can you "read off" a phrase that the model was trained on using any less computation than running the full model would require?
- **Architectural Variations**
  - Try out some variation on a common ML technique. If you're interested in this sort of project, ask me and I can explain those ideas or provide some others. For example, I have a description of [research projects](research/) that needs updating.
  - Experiment with some variations on a popular architecture (like the Transformer). We might find a shared code-base to use for this, and each project can focus on a different variation. Some ideas:
    - It’s kinda strange that the main job of the transformer is to transform the current token into the next, by residuals. … what about letting any pair of tokens subtract? 
    - What might happen to performance if...
      - we included a key with a value that's always zero?
      - each layer could query the prior layer?
      - different layers had different numbers of heads?
    - Try out different activation functions (stairsteps?)
    - Are there simpler networks that can do the same thing as transformers?
      - Smaller heads?
      - Fixed weights?
      - Hardwired data flows?
  - Experiment with different ways of training. 
    - sequence: Starting with cartoon images? Child-directed speech? Different subsets of *The Pile* first?
    - task: model a document in reverse. What if each document starts with a special token that indicates whether the text is presented forward or backward? Does pretraining on this task help any downstream tasks? Related [post on the fastai forum](https://forums.fast.ai/t/pre-trained-language-model-for-texts-that-are-read-backward/87486).
    - task: Humans, like like language models, have trouble remembering where an inspiration comes from. Give the LM some episodic memory? Predict where the current text is coming from. Something else in the context. Prior text?
