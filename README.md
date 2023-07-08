# Code Explain (`CodExp`)



Understand your codebase with static code analysis and LLM agents

![](assets/codexp.jfif)

![](assets/termination.gif)

## Plan

Use statement:

```
As a user, I want to ask questions about my entire codebase, which means the codebase is a graph, and I can ask questions about the graph.
```

current methods:
- split code into functions, and ask questions about functions

my method:
- split code using langchain, then let the model summarize in its own words
- when the LLM gets a new question, there are 2 options:
    - use regular retreival
    - summarize the README
    - use the graph retreival, meaning it will traverse the graph until it's confident enough (and there must be a way to stop it from going forever)

## Flow

this flow is supposed to try to mimic human behavious

https://whimsical.com/process-of-understanding-a-codebase-G8P3T5QgshUYjj8FYCFbFT


## Agent actions

- `jump_to_definition()`
- `google_search()`
- `readme_search()`

## Expected usage

example input and output:

```sh
$ codexp ingest path/to/repo/ --create-summaries --create-graph

>>> indexing path/to/repo/README.md
>>> indexing path/to/repo/file1.py
...
>>>
```


```sh
$ codexp chat path/to/repo/ --actions jump_to_definition,google_search,readme_search

>>> CodExp 🤖: Hello, I'm CodeExp, your codebase assistant. How can I help you?
>>> User: What is the definition of `foo`?
    [debug]: ⚙ embedding searching for "What is the definition of `foo`?"
    [debug]: matched file1.py:10:34
>>> CodExp 🤖: `foo` is defined in `file1.py` on lines 10 to 34, we can see that it calls `bar()`, and bar.
                ⚙ running action: jump_to_definition(file1.py::foo)
```

<details>
  <summary>Development details</summary>
  
## Resources

- [ ] https://python.langchain.com/docs/use_cases/code
- [ ] https://python.langchain.com/docs/use_cases/code/twitter-the-algorithm-analysis-deeplake
- [ ] https://python.langchain.com/docs/use_cases/code/code-analysis-deeplake
- [ ] https://medium.com/@neviogomez91/analyze-your-code-with-a-local-gpt-model-using-langchain-chroma-dd869d3fcdfa

## TODO

- [ ] CLI
- [ ] benchmarks against other code understanding repos. Axis: speed, accuracy, language support, ease of use
    - [ ] Eunomia
    - [ ] copying and pastingi to GPT4
    - [ ] GitHub Copilot X
- [ ] UI
- [ ] visualizing the codebase https://markgacoka.medium.com/how-to-visualize-your-codebase-7c4c4d948141
- [ ] 

</details>


```
 ______     ______     _____     ______     __  __     ______  
/\  ___\   /\  __ \   /\  __-.  /\  ___\   /\_\_\_\   /\  == \ 
\ \ \____  \ \ \/\ \  \ \ \/\ \ \ \  __\   \/_/\_\/_  \ \  _-/ 
 \ \_____\  \ \_____\  \ \____-  \ \_____\   /\_\/\_\  \ \_\   
  \/_____/   \/_____/   \/____/   \/_____/   \/_/\/_/   \/_/   
```
