---
title: "Exercise 376.3: Course Advisor Bot"
revised: 2025
---

This exercise is focused on prompting and structured output techniques to attempt to make a useful and reliable system out of an LLM. This exercise will allow you to demonstrate the following course objectives:

- [MS-API-Integration](objective)
- [MS-LLM-API](objective)
- [MS-LLM-Prompting](objective)
- [MS-LLM-Advanced](objective)
- [MS-LLM-Eval](objective)
- [CI-LLM-Failures](objective)

The fancy (resume/buzzword) name for what we're going to do here is [Agentic RAG](https://arxiv.org/abs/2501.09136). But we're going to [own our control flow](https://github.com/humanlayer/12-factor-agents/blob/main/content/factor-8-own-your-control-flow.md) rather than letting the LLM fully drive the interaction. We're also going to be practicing engineering techniques to make the system reliable and measure its performance.

## Task: Make a course advisor bot

We'll try to create a chatbot that can help students choose courses according to their interests and goals, using retrieval-augmented generation (RAG) techniques to query the course catalog.

You may choose to do this as a Streamlit app or a Jupyter notebook.

Here's how I approached it:

First, I defined a set of "tools" that the bot can use, for example, a tool that can query the course catalog and a tool that can recommend a set of courses. (Note that tools are just structured outputs, so we don't need the model to specifically be trained to "use tools".)

Then, I wrote a function that basically did the following:

```python
def get_courses_matching_interests(interests):
    messages = [{
        "role": "system",
        "content": "# System message describing the goal, the tools available, and guidance for the conversation.
    }]
    messages.append({
        "role": "user",
        "content": interests
    })
  
    # Get search queriers from the LLM
    search_query_tool = do_llm_call() # with Search Query output format required
    messages.append({
        "role": "assistant",
        "content": search_query_tool.model_dump_json()
    })
    # Search for courses matching the queries.
    courses = search_courses(search_query_tool.queries)
    messages.append({
        "role": "user",
        "content": format_courses(courses)
    })

    if len(courses) == 0:
        # Repeat the previous request, so the model can try a different search.
    

    # Get recommendations from the LLM
    recommendations = do_llm_call() # with the Recommendations output format required

    return recommendations
```

We'll walk through the LLM calls and the course search process below.

## Part 1: Structured Output from an LLM

When we're making a larger system out of component modules, it's critical that each module have a well-defined interface. Fortunately, we can *constrain the LLM* to generate responses of a desired format. 

Start by getting an OpenAI-compatible LLM endpoint. Here's a few options:

1. Use the OpenAI API (e.g., `gpt-4o`), but that will cost money. So...
2. Use a free Google Gemini API key (but the OpenAI API), as described in [CS 375 Homework 2](/units/ml-systems/chat_api_intro). Or:
3. Run locally, using Ollama.

I'd recommend Ollama, because (1) it's actually running on your computer, and (2) you'll be constrained to smaller LLMs, so prompt engineering will make a bigger difference. To do this:

1. Install `ollama`.
2. Start the server: `ollama serve`.
3. Pull the model: `ollama pull gemma3:1b-it-qat`

> If you have a lot of memory, or a good GPU, you can try `gemma3:4b-it-qat`.

If you do this, you can use:

```python
from openai import OpenAI
client = OpenAI(base_url="http://localhost:11434/v1", api_key="ollama")
model = "gemma3:1b-it-qat"
```

### Test that your model is working

```python
completion = client.chat.completions.create(
    model=model,
    messages=[
        {"role": "user", "content": "What is the capital of France?"},
    ],
)
print(completion.choices[0].message.content)
```

### Structured Output

A common library for working with structured data in Python is Pydantic. It allows you to define a data model (not to be confused with an AI model) and then validate that the data you get from any source (an API result, an LLM call, etc.) matches that model.

Here's an example Pydantic model for a search query:

```python
from typing import Literal
from pydantic import BaseModel

class SearchTool(BaseModel):
    tool_name: Literal["search_course_catalog"] = "search_course_catalog"
    thinking: str
    queries: list[str]


example_search = SearchTool(
    thinking="The user wants to know some trivia.",
    queries=[
        "What is the capital of France?",
        "What is the largest mammal?",
    ])

print(example_search.thinking)
print('; '.join(example_search.queries))
```

And here's how we might use it in an OpenAI-compatible LLM call:

```python
completion = client.beta.chat.completions.parse(
    model=model,
    messages=[
        {"role": "system", "content": f"""Write 10 search queries."""},
        {"role": "user", "content": "I'm looking for courses related to AI."},
    ],
    response_format=SearchTool,
    temperature=0.5
)

event = completion.choices[0].message.parsed
event
```

Observe that the `response_format` parameter is set to `SearchTool`, which means the LLM will be forced to output JSON that matches the `SearchTool` schema.

Try making the following changes to the system prompt and see how they affect the output:

#### Add an example

For in-context learning, it can sometimes be helpful to provide examples of the kind of output that you expect. But it can also sometimes lead to the model getting fixated on your specific examples. Try it out by adding an example to the system prompt. Try adding something like:

```
Example:
Student interest: "art"
Queries: ["art", "photography", "visual rhetoric", "painting", "sculpture", "art history", "graphic design", "digital media", "art theory", "contemporary art"]
```

How useful was adding this example?

#### Add additional instructions

You might try adding a "notes" section to the system prompt to give the model additional guidance. For example, you could say:

```
Notes:
- Before responding, write a short thought about what kinds of courses might be relevant to the user's interest.
- Assume that queries will be run against a specific course catalog, so avoid general terms like "course" or "department".
- Ensure that each query would match the title or description of one or more specific courses in an undergraduate program
```

Did these notes help the model produce better output? How would you measure that?

#### Add the output schema

You might add (within the `f`-string):

```
The output should be JSON with the following schema: {json.dumps(SearchTool.model_json_schema())}
```

Overall, which of these changes was most helpful for getting the model to produce useful output? Are there any other changes you could make? Refer to our course readings on prompt engineering for more ideas.

## Part 2: Search the Course Catalog

Now we need to find courses that match those queries.

To keep it fast and simple, we'll use a local mirror of the course catalog.

- I found a list of course sections that will be offered in FA25 by inspecting what Network requests were made by the [Calvin Course Offerings](https://calvin.edu/registrars-office/advising-registration/course-offerings) tool.
- To avoid hitting their site too hard, I downloaded that JSON file and mirrored it [here](https://cs.calvin.edu/courses/cs/375/25sp/notebooks/AY25FA25_Sections.json)

Here's how to load that file and search it:

```python
import requests

sections_json = requests.get(sections_json_url)
sections_json.raise_for_status()
sections = sections_json.json()

example_section = next(section for section in sections if section['SectionName'].startswith('CS 108'))
print(example_section)
```

The listing is by *section*, so it'll be helpful to organize by *course* instead:

```python
course_descriptions = {
    section['SectionName'].split('-', 1)[0].strip(): (section["SectionTitle"], section["CourseDescription"])
    for section in sections
    if "CourseDescription" in section
    and section.get('AcademicLevel') == 'Undergraduate'
    and section.get('Campus') == 'Grand Rapids Campus'
}

print("Found", len(course_descriptions), "courses")
print(course_descriptions["CS 108"])
```

Here's a function to find courses matching a query:

```python
def search_courses(query: str):
    """
    Search for courses that match the query.
    """
    query = query.lower()
    matches = []
    for course, (title, description) in course_descriptions.items():
        if query in title.lower() or query in description.lower():
            matches.append((course, title, description))
    return matches
search_courses("programming")
```

If you have multiple queries, you might want to combine the results:

```python
def find_courses_matching_queries(queries: list[str]):
    """
    Find courses that match any of the queries.
    """
    return set(
        course
        for query in queries
        for course in search_courses(query)
    )
find_courses_matching_queries(["programming", "AI"])
```

## Part 3: Recommendations

Here's my suggestion for a recommendation output format:

```python
class CourseRecommendation(BaseModel):
    course_code: str
    course_title: str
    course_description: str
    reasoning: str

class RecommendTool(BaseModel):
    tool_name: Literal["recommend_course"] = "recommend_course"
    thinking: str
    recommendations: list[CourseRecommendation]
```

Now you put it together to make a course advisor bot!

## Part 4: Testing

Test your bot with a few different student interests. Measure at least the following:

- How often does it fail to respond, or give poor results?
    - can you fix this, e.g., by changing the system prompt?
- Latency of the system, broken down by part. (which part is slow? Does that make sense?)
    - can you improve this, e.g., by changing the input or output formats?
- Are the search queries relevant for the student's interest?
- Are the courses returned relevant for the search queries?
- Are the recommendations relevant for the interest?

You'll have to think about how to measure this. You might want to ask a few friends to try it out and give you feedback.

Think about how you could improve the system.
