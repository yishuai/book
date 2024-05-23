如何请 AI 做事？

I originally compiled it based on the prompt engineering portion of the 2.5 hour NurIPS tutorial。
I’ve added several enrichments and examples since. While the talk is not available online, these comprehensive but quick notes hopefully provide a good, quick overview :) 

### Tip #1: Write clear and specific instructions

**Give detailed context** for the problem. Reducing ambiguity reduces the likelihood of irrelevant or incorrect outputs. 

You can also **use delimiters** to clearly indicate distinct parts of the input. For example: section titles, triple quotes, triple backticks, triple dashes, angle brackets, “####”

**Specify the desired output format or length of output**.

One method is to ask the model to adopt a persona. For example: 

“Pretend you’re a creative writer”

“Respond in roughly two sentences.”

“Give me a summary of this text. Here are examples of summaries that I like ___”

**Provide examples.** For example, these are the steps for few shot prompting. 

1. First example (first “shot”): Give an example of a prompt and corresponding output/response. 
2. Second example (second “shot”): Give a second example of a prompt and output. 
3. Your prompt: Give your actual prompt. Now, your model can follow the pattern established by the first two examples.

### Tip #2: Give the model time to think

Models make more reasoning errors when they respond immediately. 

By **asking for a chain of reasoning**, this prompts the model to think incrementally and more considerately. You can ask for a “chain of thought” or specify the specific steps. This simple addition to the prompt famously works well: **“Think step by step.”**

For example, if you’re asking the model to grade a student’s solution, you could prompt the model:

- Step 1: work out your own solution to the problem
- Step 2: compare your solution to the student’s solution
- Step 3: finish calculating your own solution before evaluating the student solution

### Tip #3: Prompt multiple times

Ask the model to answer a question multiple times and determine the best answer. When accuracy is most important (and not latency or cost), generate multiple responses with different prompts.

Here are some things you can adjust:

- **Temperature**: regulates the randomness or creativity of the LLM’s response. Higher temperature gives more varied, creative responses. Lower temperature gives more conservative, predictable responses.
- **Shots**: refers to the number of examples (”shots”) given in the prompt. Zero-shot refers to providing no examples, one-shot refers to providing one example, etc.
- **Prompt**: being more or less direct, requesting explanations, drawing comparisons, etc.

### Tip #4: Guide the model

Here are some examples:

- **If the document is too long,** the model might stop reading early. You can guide the model to process long documents piecewise and construct a full summary recursively.
- **Help it self correct.** If the model starts incorrectly, its hard to self correct. "I've received an explanation about quantum physics from you, are you sure about your answer? Can you review it and provide a corrected explanation starting with the basics of quantum mechanics?”
- **Don’t ask leading questions.** The model is eager to please, so guide but leave prompts open-ended.
    - "Do video games cause violence?” ❌
    - “I'd like an unbiased overview of the research findings on the relationship between video games and behavior.” ✅

### Tip #5: Break down the task or prompt

**Break down complex tasks to be multiple, simple tasks.** This helps because complex tasks have higher error rates than simple tasks.

You can use **intent classification** to identify the most relevant instructions, then combine the responses to create a cohesive output. For example:

- **Query:** "I'm going to Paris for three days, and I need to know what to pack, the best places to eat, and how to use public transportation."
- **Breaking Down:**
    - Intent 1: What to pack for a trip to Paris.
    - Intent 2: Recommendations for the best places to eat in Paris.
    - Intent 3: Guidance on using public transportation in Paris.
- **LLM Response:** The AI would tackle each intent separately, providing tailored advice for packing, dining, and commuting in Paris, and then integrate these into a comprehensive response

Or, if the subtasks are connected, 

- Step 1: Take task and break it down into queries
- Step 2: Feed the output from the first query into the next query

*** note: this can also reduce costs because it will be a smaller cost at each step*

### Tip #6: Use external tools

As a rule of thumb, **if a task can be done more reliably or efficiently by a tool rather than a language model, offload it** to get the best of both. 

Here are some example tools:

- **Calculator:** LLMs are bad at math. By nature, their goal is to generate tokens/words, not numbers. Calculators can significantly improve the LLM’s math ability.
- **RAG: C**onnect the LLM to intelligently retrieve information instead of trying to fit it into the context window. For example, **[Metaphor’s](https://metaphor.systems)  web search retrieval API** 😉 — email me for free access haha
- **Code execution: U**se code execution or call external APIs to execute and test code created by the model.
- **External functions: D**efine functions for the model to write calls to. For example, send_email (), get_current_weather(), get_customers(). Execute these functions on your end and return the response to the model.

## 参考

- OpenAI [Prompt Example](https://platform.openai.com/examples) 
- Andrew Ng and Open AI’s Isa Fulford, “Application Development Using Large Language Models” tutorial at NeurIPS (Dec 11, 2023), [分享笔记](https://mphr.notion.site/Prompt-Engineering-Best-Practices-0839585d4bce4c6abb0b551b2107a92a)