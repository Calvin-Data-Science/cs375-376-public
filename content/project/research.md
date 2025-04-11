---
title: "Research Projects"
---

Professor Arnold is willing to advise one of the following research-y projects. Others may be permitted if you have a very clear proposal, discussed well in advance.

(You may notice some commonalities among these ideas. That's intentional.)


### Decompose and Recompose Complex Sentences using Simple Sentences

Writers sometimes like to write really long and complicated sentences because those are the first things that come to mind and it's easy to just keep typing and get your ideas out there but it's not really clear what you're trying to say and you're thinking while you're writing so you end up with this big long train of thought that's hard for people to follow and it would be really helpful to readers if the writer could split the big sentence apart into little sentences that are simpler but sometimes there are actually complicated things that the writer is trying to explain and the simple little sentences get hard to follow so we don't necessary want to do this entirely automatically so it would be helpful to have the writer stay in control of this process. So:

- **Task 1**: Complex input sentence in, set of simpler sentences out.
- **Task 2**: Set of simple sentences in, combined sentence out.

Possible dataset: [BiSECT Dataset | Papers With Code](https://paperswithcode.com/dataset/bisect). There are also "sentence combination" exercises that language students do; there are probably some datasets from those.

### Predictive Text from Very Rough Drafts (e.g., rambling speech)

Speech recognition technology is a powerful and efficient way to enter text on a touchscreen device, but many people don't use it. One reason is that it is cognitively challenging: you must think of exactly what to say, and how to say it clearly enough to be understood, on the first time, potentially in a distracting or non-private environment. But what if you could first "think out loud" about what you want to say, perhaps whispering a stream of consciousness to your phone---then your phone would give you (a) an outline of the main points you wanted to say and (b) really accurate predictions about what word to type next in order to say it?

-   **Input**: a "stream of consciousness" rambling about something you want to communicate, likely already in text form (perhaps by a low-quality speech recognizer)

    -   Training data could be generated automatically by corrupting ground-truth outputs in various ways.

-   **Output**: a prediction of the next word to be typed in the final message you want to send.

### Other language tasks

- Paraphrasing using any-to-any translation
- Mining Wikipedia edit history (or other datasets, like Newsela) for data on editing language
- Language models that learn to generate "blanks" that a writer would need to fill in

### De-EQ

Given a sound corrupted by a random EQ curve or other processing step, predict the parameters for that processing step. *This kind of task is called [self supervised learning](https://lilianweng.github.io/lil-log/2019/11/10/self-supervised-learning.html).* See Microsoft's [HEXA](https://www.microsoft.com/en-us/research/blog/hexa-self-supervised-pretraining-with-hard-examples-improves-visual-representations/).