---
title: "Forum Posts 22SP"
---

## Wrap-Up

**Have you done your course evals?**

### Projects

- Showcase is next Thursday 9am in our normal lab space.
  - There are about 18 projects, so we will divide into 5 clusters of 3 or 4 projects each.
  - Everyone will demo their work to the others in their clusters.
  - Each cluster will pick one or two projects to present to the whole class.
  - Everyone is expected to attend; Effort points will be awarded.
- Revised specs are on the website, including [grading](https://cs.calvin.edu/courses/cs/344/22sp/project/#grading) and some detailed [pointers on how to do an "expository notebook" project](https://cs.calvin.edu/courses/cs/344/22sp/project/replication/#expository-notebooks-notebookify).

Also, several projects might benefit from using [captum](https://captum.ai/tutorials/) (for interpreting model predictions) and [streamlit](https://streamlit.io/) (for an extremely easy way to make AI-powered web apps).

### Optional Homework

As mentioned in class, I've posted an *optional* [homework](https://cs.calvin.edu/courses/cs/344/22sp/units/13hcai/homework/). It's pretty practical and hands-on, and may actually help some people with their projects. You can choose to use it to replace any of your other mastery grades, including the project grade. (You don't have to specify which one, I'll just configure Moodle to drop the lowest.)

If you started it already, I made a minor revision: the example Transformer model now implements multi-head attention. (I couldn't stop myself.)

### Summer Opportunities

I'm running an open summer research team on applying language models to help people communicate. At least 8 people have expressed interest in participating in some way. I'd like to invite you to join us. There are two parts to consider:

1. I'm going to be teaching an unofficial "May intensive" (aka bootcamp), starting May 9, for the summer team. The goal is to bring everyone up to speed on language modeling with Transformers and some basic web development. We'll get our hands quite dirty (replicating a research paper from scratch and building a web UI for it, for example). We'll have some students who haven't done much CS and some who are coming from this class, so it should be a diverse crowd!
2. After the intensive, we'll break out into small groups to do projects. If you've wanted to do an AI project beyond the constraints of this class, here's an opportunity. Participating in the intensive is highly recommended but not strictly required for this part.

If you're interested in either part, please let me know!

### Grading

Sorry I'm still behind on grading. Since this means that you haven't had the revision opportunities for a few assignments, I'll be extra lenient when assigning final grades.

### Feedback

The course evals give only a narrow view of your experience with this course. More feedback will help us continue to improve. **Simple way to leave anonymous feedback**: reply to this Piazza post.

Thanks for a great semester, and see you Thursday!

## Week 13: Finishing RL, Starting Human-Centered AI

What happens when AI meets people? We've been discussing this informally throughout the semester (haven't lately because nobody signed up to lead a topic!). This week we'll start asking: how can we ensure that AI results are

- Correct,
- Just, and
- Useful?

We'll start this week with how we might convince ourselves that model outputs are (or aren't) *correct*. But we have some important things to wrap up from our brief intro to Reinforcement Learning, so we'll tackle that on Monday.

Notes:

- **Project**: Your next milestone is a 15-minute meeting with me sometime before Reading Recess. [Sign-up page](https://outlook.office365.com/owa/calendar/Arnoldmeetings@calvincollege.onmicrosoft.com/bookings/s/u-L9xl9pHkOh-NBDCyyiNA2).
- **Prep 13** is posted. Remember to finish Prep 12; you have a few more days until it closes.
- **Homework**: Homework 12 is a Fundamentals notebook to help think about and practice the different sequence models we've been looking at. I really enjoyed making it, and I hope you enjoy going through it.
  - There may be some things about it that aren't quite clear, since some of the topics get advanced. Please ask questions on Piazza or in class!
  - Want extra practice with anything we've done so far? I have a bunch of notebooks that I didn't get finished in time for this year. If your current project isn't working out well, you could even make a project out of turning a few of them into exercises for next year. Let me know if you're interested!
  - Did you miss last week's homework quiz? Message me and I can open it back up.
- **Discussion**: The PaLM paper I showed in class will actually be the subject of a Discussion for this week. As such, it'll be due at the usual Discussion due time (Wednesday). See Moodle.


## Week 12: Review and Reinforcement Learning

Happy Saturday everyone!

This coming week we'll be reviewing some things and then moving on to Reinforcement Learning, the engine behind models that have learned to play games like Go and Starcraft, and also behind some kinds of robotics (self-driving cars?). The plan after this week is to discuss human-centered topics like fairness, transparency, and HCI. (If there's a topic you've been wanting to learn about, now is the time to let me know!)


Notes:

- Please fill out the [feedback survey for our guest lecture](https://forms.gle/HQs6nap2Y1ngzJoQA) by class time Monday if you haven't yet. This is important because it helps us make decisions about future instructors.
- There's a **Prep** activity and quiz to do; by Friday should be fine.
- **Project**
  - If you need more compute for your final project, you can use Calvin's supercomputer, [Borg](https://borg.calvin.edu). You should all have received an email from Chris about setting up your account. I've written some [notes on the Resources page](https://cs.calvin.edu/courses/cs/344/22sp/resources/#borg-supercomputer) about how to run our software on it.
  - I'm working on project feedback. We'll have another milestone the following week.
- **Homework**: For homework for this week, I've posted a Study Quiz that closes at homework due time. It's an Effort grade only.
  - Sorry I didn't get a Fundamentals ready in time this week either. If you're interested in getting extra practice with the code behind what we were working with last week, you can work through the rest of the notebook that we worked with on Monday.
  - I haven't posted a Reflection because it was the part of the course that most people who took the mid-semester survey found least helpful. But for those who *have* found it helpful, you can write up your reflections informally and share them with me for feedback.


## Week 10: Transformers (self-attention)

This coming week is advising week, which means we take a break on Wednesday. I also reduced the intensity of other things we're doing, so hopefully you can take a good break to celebrate figuring out Workday Student!

You've now seen that Transformers-based models can do pretty neat things with text, and you've probably heard about how they're taking over in image processing, audio, reinforcement learning, and more. What's the secret to their success? Many researchers think it's an element called "attention". It's actually a pretty simple idea: instead of the input to one block always coming from the same other block, the blocks get to choose which data to use as their input using a classifier. But there's a lot to unpack about that idea. So we'll take our two class days this week to do that.

A few things:

- Last week would have been another Reflection week, but we skipped it in favor of an anonymous [Mid-Semester Survey](https://forms.office.com/Pages/ResponsePage.aspx?id=uUljdRAGAUuReypKwQ35Rw0bDGF2ImlDp6FjI7QrXehUMUtET1YyOFk0MFkzSTVISk9OR1I4RllETC4u). It will probably take 5 minutes or less to complete, and your input will help improve the class (at least next year, and maybe even the rest of this year too).
- I've put up a few Study Quizzes (see top of Moodle) to help review material from earlier in the class. They're all from the first couple of weeks; more are coming (especially since now some of you have given some ideas!). They are short and low-stakes; I haven't yet decided if they should be entirely optional or not.
- I've learned that the Mastery grades aren't showing up on the individual assignments for some people--and the gradebook is only showing the bad-looking numeric grades instead of the scale I configured. I'm working with CIT to figure out what's going on. If there's anything else that seems wrong about the grading so far (besides some things that I haven't gotten to grade yet showing up as Dropped), let me know!
- Prep 10, Discussion 10, and Homework 9 are due this week as normal, though both the Prep and the Homework are intended to be shorter than normal.

See you Monday!

## Week 9: NLP Modeling

Welcome to week 9! This is the week we get to dig into Transformers and see how it works. I've found these models really useful and cool to think about because you can be so creative with how you use them. I hope this week you get a bit of a taste of that---and maybe a desire to play with them for your final project (see the Projects page for the research projects I'm offering for this class).

A few things:

- **Masks in class**: As mentioned last class, I'm planning to make class "masks optional". If you have any concerns about this, please let me know and we can back off. Of course you may decide day by day; for example, if you have a cold, or live with someone who does, I'd encourage wearing a mask.
- Due this week (you can always look at the [Moodle calendar](https://moodle.calvin.edu/calendar/view.php?view=month&course=55940))
  - **Prep 9**. The assignment includes a "study guide" of some questions to help you focus your thinking. I'm not expecting anything turned in, but I'd be very happy to chat about anything you're unclear about.
  - **Project Proposals**. I'm really looking forward to reading these!
  - **Discussion 9** posts and replies. Also, please **[sign up](https://calvincollege.sharepoint.com/sites/Section_81629/_layouts/15/Doc.aspx?sourcedoc=%7BC84B7BF4-354E-44EE-B329-BEAB4FA69EDC%7D&file=Discussion%20Topic%20Signup.xlsx&action=default&mobileredirect=true) for a topic**; we have some blank spots coming up!
  - **Homework 8**
- Student Senate sponsors coffee or lunch with profs. I like coffee and lunch, and I like talking with you, so that sounds like a great idea. Anyone interested?

## Week 7: Embeddings

Welcome to unit 7, the week before Spring Break!

In this unit we introduce one of the most powerful concepts in machine learning: the *embedding*. It's the idea that instead of being explicitly given a representation for something, we *learn* it from data *based on the properties it should have*. We've actually already seen embeddings of various kinds (the inputs to the last layer of an image classifier for one), but we'll look at two examples where the embedding aspect is even clearer: movies and words.

Some logistics:

1. I made some late updates to Preparation 7, and posted the quiz late, so it's okay if you don't get to it until Wednesday.
2. Homework 6 is due on Thursday. It's not the mini-project I'd hoped because I thought that would be too much, but it gets you pretty close. (If you're interested in trying that mini-project anyway, I wrote up some [instructions](https://cs.calvin.edu/courses/cs/344/22sp/units/06recap/mini-proj/) for it.)
3. I recorded a video demo of how backprop works; see our [Walkthroughs folder in Teams](https://calvincollege.sharepoint.com/:f:/s/Section_81629/EiZcXdth0VZMhjz4S_69w0oByq-i_tuvqJMm1VgDMjNtJw?e=YHcM0a).
4. Reflection 3 is due on *Friday*. It's the same structure as last week: write your own quick summary of all the learning objectives from the past two weeks.
5. In lieu of a normal Discussion this week, we get to start thinking about **project ideas**! I've put up a Forum on Moodle for this week if you'd like to pitch an idea and are looking for partners. We'll talk more about projects in class this week; here's the [overall description](https://cs.calvin.edu/courses/cs/344/22sp/project/).
6. I've fixed up the gradebook, so now would be a good time to check where you stand. (I haven't gotten to all of the revisions yet.) Things I haven't graded yet should show up as "dropped", but if there's anything that's missing or too-low and not "dropped", please let me know.

See you Monday!

## Week 6: Recap and Regularization

In this unit, after reviewing where we've been, we push towards state-of-the-art models (still focusing on computer vision). We’ll introduce or revisit tools that allow our models to achieve high performance, such as data augmentation and regularization. Finally, we’ll get more practice with how neural networks work from the ground up as we implement our own simple neural net image classifier from scratch (definitely something to mention in an interview!).

Logistics are basically as usual:

- Prep 6 for Monday (note that the quiz is always open for an extra week, but do remember to come back to it!)
- We'll do Fundamentals work during lab time again, so no separate Lab due this week.
- Discussion 5 for Wednesday as usual.
- Homework 5 is 3 more Fundamentals notebooks, due Thursday as usual.
- No reflection this week (they're every other week).

I had gotten behind on answering your questions; here's some [Q&amp;A from week 5](https://cs.calvin.edu/courses/cs/344/22sp/units/05learning/qa/). And I'm still behind in feedback too, my apologies.

## Week 5: Learning

Happy Saturday! We're making good progress getting under the hood of how neural nets work. **Last week** we tackled regression; we introduced *linear layers* as the basic building blocks of neural nets, *gradient descent* as general way to find good values of parameters, and *backpropagation* as a general tool to compute gradients efficiently and without numerical issues. **This week** we extend to *classification*, where we'll learn about some *non-linear* layers, which are where neural nets get their power.

Logistics!

- Prep 5 should be done by Monday's class as usual.
  - To be honest, we won't get to much of that material until Wednesday, though. So feel free to wait till then even to submit the quiz.
- Discussion 4 is due Wednesday; same instructions as last time, just different topic.
- Homework 4 and Reflection 4 are both due next Thursday.
  - We've shifted the due date for Reflections so that the reflection can include everything you've done related to the week's learning objectives.
  - Homework 4 introduces a kind of assignment you may have heard about from last year's students: the Fundamentals notebook. These were a consistent student favorite last year, so I'm bringing them back! Future homework assignments will include a mix of narrative and Fundamentals tasks; this one is just Fundamentals.
- The Syllabus has been updated to reflect simplified logistics and grading; it should be much more clear now.

See you Monday!

PS - Here's an example of a very non-neural [AI to solve Wordle](https://aditya-sengupta.github.io/coding/2022/01/13/wordle.html). Neural nets are great tools for handling *perception* tasks, but not all tasks are perception tasks.

## Week 3: Data, Ethics Intro

Happy Saturday everyone!

We were trying to go too fast, so I delayed starting on Chapter 4 by a week. If you've already started on Chapter 4, that's great; it's a dense chapter, so more time on it will help.
Instead, this week we'll look more into data and also how we evaluate AI systems. See [this week's page](https://cs.calvin.edu/courses/cs/344/22sp/units/03models/) for more details.

At this point, everything from Week 1 should be done, plus Preparation 2 and Lab 2. **Reminder**: Preparation exercises and the quizzes are due the Monday night of the corresponding week. They close on Moodle a week later than that only to avoid having to track late submissions.

This week:

- Prep 3, including the quiz, is due Monday. It's substantially smaller than it used to be (reload the page if chapter 4 stuff still shows up).
- Homework 2 is due Tuesday. You may need to come to lab on your own time to finish it up.
- Discussion posts are due by class time on Wednesday (this had been incorrect on Moodle, sorry). **Come to class prepared to discuss an interesting point that someone else raised.**
- Our first **Reflection** is due on Wednesday.
- I'm considering having a check-in quiz this week; if so, that will be on your own time and probably open on Thursday.
- We'll work on Homework 3 on Friday.

I look forward to seeing everyone on Monday!

## Week 2: Data

Congratulations on making it through the first week of classes in yet another unusual semester. We covered a lot of ground in the first week! Just look at the [objectives](https://cs.calvin.edu/courses/cs/344/22sp/units/01introduction/) to jog your memory.

### Wrapping up Week 1

- Make sure you've done all of the following (check them off in Moodle when you have)
  - **welcome survey**
  - **Python warm-up quiz**
  - **Preparation 1** (reading and quiz)
  - **Discussion 1**
  - And make sure you've logged onto **Piazza** (just click the link on Moodle).
- Homework 1 is to finish Lab 1.
  - We encountered some difficulty with the Image Classifier part because of a bug in a library we're using. See the "Hotfix" instructions in the [lab description](https://cs.calvin.edu/courses/cs/344/22sp/units/01introduction/lab/) for what to do about this.
    - Even if it worked for you, still check for the temp folder.
  - We'll allow some of the time in Monday's lab to wrap up the Image Classifier part of Lab 1.
  - If you want to work on your own time, you can come into the lab; everything should work over Guacamole too, though availability is limited.
  - I've bumped the due date to Tuesday.
- We will not have a Reflection or Project Milestone for this week.

### Preparing for Week 2

In week 2 we will start considering what *data* you need to train models. You'll collect some image data yourself and train and evaluate a model. We'll also start looking at some of the ethics of collecting data for AI; we will return to this discussion throughout the semester.

- On **Monday** we will do Lab 2 (with a bit of time to finish the part of Lab 1 that is highly related), where we'll try out some variations on the image classifier and also look a bit at the data it's using.
  - Please read Chapter 2 and some of Chapter 3 in preparation. See Moodle for a reading quiz.
- On **Wednesday** we'll review what we've been studying in a lecture format.
- On **Friday** we'll wrap up what we didn't get to on Wednesday, planning to leave time to work on Homework 2 (training a classifier on your own images).

I’m here for you. We’re all here for each other. May our Lord give us all strength to persevere, joy in the journey, and love for each other along the way.
