---
title: "Chat Completions APIs"
revised: 2025
---

Objectives:

- I've called the OpenAI Chat Completions API to generate text.
- I can explain what the inputs and outputs of the Chat Completions API are, especially its "messages" data structure.

## Getting an API key

You'll need an API key to access most LLM APIs. For this activity, we'll use the OpenAI Chat Completions API - but we don't necessarily need an OpenAI account! Several companies provide APIs that are compatible with OpenAI's API format.

Think of it like phone chargers: even though we often call them "iPhone chargers" or "Android chargers", any USB-C charger works with any USB-C device. Similarly, we can use any API that's "OpenAI-compatible" with code that expects to talk to OpenAI's API.

You have two options for getting an API key:

1. OpenAI: Create an account and add a few dollars of credit
2. Google AI Studio: Get a free API key that works with OpenAI-compatible code at [Google Gemini API key page](https://aistudio.google.com/app/apikey)

Easiest is to use Google Colab's Secrets tab.

**Important**: Save your API key in a safe place. You'll need it to access the API, and the page only shows it once.

## Setting up your API key

Before running any code, you need to store your API key in a `secrets.toml` file. This file should never be committed to version control. It lives in a special folder named `.streamlit` in your project directory.

Create a `.streamlit/secrets.toml` file with this content:

```toml
OPENAI_API_KEY = "your-key-here"
```

If you're using the Google Gemini API key, use the same format; the code will still look for `OPENAI_API_KEY` since we're using the OpenAI-compatible interface.

## Using an LLM to generate starter code

First, choose what task you want to have the AI do. Here's a few I've tried:

- The user describes their reflections on something going on in their life, and the AI provides Scripture-grounded reactions.
- The app uses the OpenAI API to play a game of tic-tac-toe with the user.
- The user provides an image and the app makes a table of the items in the image with a detailed description of each one and its location in the image.
- The user pastes an essay they're working on and the AI coaches them on how to improve it.

Once you've chosen a task, use a chatbot to generate some starter code. For example, I prompted Claude with: "Can we build a Streamlit app that uses the OpenAI API to have the user play a game of tic-tac-toe?".

To ensure that the generated code used the correct OpenAI API, I pasted an example of the setup code. Specifically, I went to [the Gemini docs on OpenAI-compatible API](https://ai.google.dev/gemini-api/docs/openai) and copied the example code snippet on that page, then at the end of the prompt I added: "Here's a code example for the variant of the API we're using." and pasted the code snippet.

Note: you might need to change the `GEMINI_API_KEY` secret to `OPENAI_API_KEY` in the generated code.

### Iterate with the chatbot

Don't treat the chatbot as a one-and-done tool; have a conversation. For example, for the tic-tac-toe game, I followed up with "The AI opponent is pretty weak. Maybe it could explain a few moves that it's thinking about before making its choice?" and then "I was getting an error because the AI response was \`\`\`json instead of the JSON object itself. That was hard to figure out because the st.rerun swallowed the error message."

## Running the Streamlit app

If you're lucky, you just got some starter code for the app you want to build. Now to run it. Two options: local or Streamlit cloud.

### Local setup

1. Install `uv`. This tool makes it really easy to manage your Python environment.
2. Create a new folder for this project.
3. Create the `.streamlit/secrets.toml` file as described above.
4. In that folder, run `uv init` and then `uv add streamlit openai`.
5. Paste the code that the chatbot generated into a file called `streamlit_app.py`.
6. Run `uv run streamlit run streamlit_app.py`. (Yes there's two "run"s in that command.)

### Streamlit cloud setup

1. Start with the [Streamlit chatbot template](https://share.streamlit.io/template-preview/b8e65aff-d8c7-4b7d-9d4c-eb79249dfc4b). Click "Use Template" in the top-right corner.
2. Click Advanced and edit the Secrets box to include the content of your `secrets.toml` file. e.g.,:
   ```toml
   OPENAI_API_KEY="your-key-here"
   ```
3. Choose whether to edit in Codespaces (in browser) or locally (clone the repo).
4. If using Codespaces, note that you may need to manually create the `.streamlit/secrets.toml` file with your API key (even though you set it in the template).

## Reflecting on the OpenAI API

Find the part of the code that calls the OpenAI API.

1. What does the input to the API look like? Write a brief description of the data structure that is used to give the user's input to the LLM.
2. What does the output of the API look like? You might add some `print` statements to the code to see the output.
3. Did the AI generate any error-handling code? What errors is it looking for, and how does it handle them?

Notice specifically that `messages` is a list of messages, both user and assistant.

Think about how you might use this API to do the code-generating task that we just did with the chatbot. Sketch out what the `messages` object might look like for a two-step conversation about generating and refining code.

## Showcase

Once you have a working app, upload it to Moodle in the provided dropbox.

Note: you don't have to include the answers to the reflection questions in your submission. They're just to help you understand the code you're working with. When using this activity to demonstrate meeting a course objective, expect to discuss these questions in a meeting with your instructor.
